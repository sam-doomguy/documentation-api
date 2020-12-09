A `GET` request to this endpoint allows you to get rule settings for all configured rules of the specified account.

If a rule has never been configured, it will not show up in the resulting data.
For example, even if our bots run rule `RDS-018` for your account hourly, if you have never configured it, it will not be part of the data body we send back.

This endpoint only returns configured rules. If you want to include default rule settings, set `includeDefaults=true` in query parameters.

**Note:** If the account contains rule settings that are marked as deprecated and have not been disabled, the following meta warning will be included in the response:

```json
{
  "meta": {
    "deprecation": {
      "warning": {
        "message": "1 manually configured rule in this account is deprecated. Refer to our Help Pages for instructions.",
        "link": "https://www.cloudconformity.com/help/rules.html",
        "rules": [
          {
            "riskLevel": "LOW",
            "id": "RuleID-001",
            "extraSettings": null,
            "provider": "aws",
            "enabled": true,
            "exceptions": { "resources": null, "tags": null }
          }
        ]
      }
    }
  }
}
```

### Rule settings

Every rule in Cloud Conformity can be configured via API. These rule settings can disable or enable rules, change
default risk level, setup exceptions and configure rule-specific settings.

Rule settings returned from `GET /v1/accounts/{accountId}/settings/rules?includeDefaults=true` endpoint
are formatted as the following example:

```json
{
  "id": "EC2-012",
  "enabled": true,
  "riskLevel": "MEDIUM",
  "exceptions": {
    "tags": ["Role::Temporary", "TagKey::TagValue", "TagKeyOrValue"],
    "resources": ["i-98f25d31", "another EC2 instance ID"]
  },
  "extraSettings": [
    {
      "name": "threshold",
      "type": "single-number-value",
      "value": 100
    }
  ],
  "configured": false
}
```

### Extra setting types

These formats are are found in `type` field of rule extra settings:

#### multiple-string-values

- **Usage:** Used when one or more strings are required.
- **UI:** List of text fields

_Example:_

```json5
{
  id: "EC2-017",
  //...
  extraSettings: [
    {
      name: "desiredInstanceTypes",
      type: "multiple-string-values",
      values: [
        {
          value: "t2.micro"
        },
        {
          value: "m3.medium"
        },
        {
          value: "m3.large"
        }
      ]
    }
  ]
  //...
}
```

#### multiple-object-values

- **Usage:** Used when one or more sets of values are required.
- **UI:** Table of text fields

_Example:_

```json5
{
  id: "RTM-01a",
  //...
  extraSettings: [
    {
      name: "desiredInstanceTypes",
      type: "multiple-object-values",
      valueKeys: ["eventName", "eventSource", "userIdentityType"],
      values: [
        {
          value: {
            eventName: "^(iam.amazonaws.com)",
            eventSource: "^(IAM).*",
            userIdentityType: "^(Delete).*"
          }
        }
      ]
    }
  ]
  //...
}
```

#### choice-multiple-value

- **Usage:** Used when one or more selections from a predefined set of values are required.
- **UI:** List of checkboxes

Note that all allowed values are returned from `GET /v1/accounts/{accountId}/settings/rules?includeDefaults=true` endpoint

_Example:_

```json5
{
  id: "RTM-009",
  //...
  extraSettings: [
    {
      name: "ConfigurationChanges",
      values: [
        {
          value: "internetGateway",
          enabled: true
        },
        {
          value: "securityGroup",
          enabled: false
        },
        {
          value: "elasticNetworkInterface",
          enabled: true
        },
        {
          value: "virtualPrivateCloud",
          enabled: false
        }
      ]
    }
  ]
  //...
}
```

#### choice-single-value

- **Usage:** Used when a single value should be selected from multiple choices.
- **UI:** List of radio buttons

Note that the allowed values differ for each rule:

- Support-001 (Support Plan)
  - "Basic"
  - "Developer"
  - "Business"
  - "Enterprise"
- EC2-025 (EC2 Instance Tenancy)
  - "default"
  - "dedicated"
  - "host"
- ELB-008 (ELB Listener Security)
  - "1" (Yes)
  - "0" (No)
- ELB-010, ELBv2-004 (ELB/ELBv2 Minimum Number Of EC2 Instances)
  - Minimum Number Of EC2 Instances
    - 1 (One instance)
    - 2 (Two instances)
- ELBv2-005 (ELBv2 ALB Listener Security)
  - Include Internal Load Balancers
    - "1" (Yes)
    - "0" (No)

_Example:_

```json5
{
  id: "Support-001",
  //...
  extraSettings: [
    {
      name: "level",
      type: "choice-single-value",
      value: "Developer"
    }
  ]
  //...
}
```

#### countries

- **Usage:** Used when one or more countries should be selected.
- **UI:** Multi-select list of countries

For certain rule settings, extra settings require configuration for a "countries" value. Value of each item is a country code.

_Example:_

```json5
{
  id: "RTM-005",
  //...
  extraSettings: [
    {
      name: "authorisedCountries",
      type: "countries",
      values: [
        {
          value: "CA"
        },
        {
          value: "AU"
        },
        {
          value: "US"
        },
        {
          value: "UM"
        }
      ],
      countries: true
    }
    //..
  ]
  //...
}
```

Below is the list of supported countries and their respective codes:

| Country Name                                 | Code |
| -------------------------------------------- | ---- |
| Other Country                                | O1   |
| Andorra                                      | AD   |
| United Arab Emirates                         | AE   |
| Afghanistan                                  | AF   |
| Antigua and Barbuda                          | AG   |
| Anguilla                                     | AI   |
| Albania                                      | AL   |
| Armenia                                      | AM   |
| Angola                                       | AO   |
| Asia/Pacific Region                          | AP   |
| Antarctica                                   | AQ   |
| Argentina                                    | AR   |
| American Samoa                               | AS   |
| Austria                                      | AT   |
| Australia                                    | AU   |
| Aruba                                        | AW   |
| Aland Islands                                | AX   |
| Azerbaijan                                   | AZ   |
| Bosnia and Herzegovina                       | BA   |
| Barbados                                     | BB   |
| Bangladesh                                   | BD   |
| Belgium                                      | BE   |
| Burkina Faso                                 | BF   |
| Bulgaria                                     | BG   |
| Bahrain                                      | BH   |
| Burundi                                      | BI   |
| Benin                                        | BJ   |
| Saint Bartelemey                             | BL   |
| Bermuda                                      | BM   |
| Brunei Darussalam                            | BN   |
| Bolivia                                      | BO   |
| Bonaire, Saint Eustatius and Saba            | BQ   |
| Brazil                                       | BR   |
| Bahamas                                      | BS   |
| Bhutan                                       | BT   |
| Bouvet Island                                | BV   |
| Botswana                                     | BW   |
| Belarus                                      | BY   |
| Belize                                       | BZ   |
| Canada                                       | CA   |
| Cocos (Keeling) Islands                      | CC   |
| Congo, The Democratic Republic of the        | CD   |
| Central African Republic                     | CF   |
| Congo                                        | CG   |
| Switzerland                                  | CH   |
| Cote d'Ivoire                                | CI   |
| Cook Islands                                 | CK   |
| Chile                                        | CL   |
| Cameroon                                     | CM   |
| China                                        | CN   |
| Colombia                                     | CO   |
| Costa Rica                                   | CR   |
| Cuba                                         | CU   |
| Cape Verde                                   | CV   |
| Curacao                                      | CW   |
| Christmas Island                             | CX   |
| Cyprus                                       | CY   |
| Czech Republic                               | CZ   |
| Germany                                      | DE   |
| Djibouti                                     | DJ   |
| Denmark                                      | DK   |
| Dominica                                     | DM   |
| Dominican Republic                           | DO   |
| Algeria                                      | DZ   |
| Ecuador                                      | EC   |
| Estonia                                      | EE   |
| Egypt                                        | EG   |
| Western Sahara                               | EH   |
| Eritrea                                      | ER   |
| Spain                                        | ES   |
| Ethiopia                                     | ET   |
| Europe                                       | EU   |
| Finland                                      | FI   |
| Fiji                                         | FJ   |
| Falkland Islands (Malvinas)                  | FK   |
| Micronesia, Federated States of              | FM   |
| Faroe Islands                                | FO   |
| France                                       | FR   |
| Gabon                                        | GA   |
| United Kingdom                               | GB   |
| Grenada                                      | GD   |
| Georgia                                      | GE   |
| French Guiana                                | GF   |
| Guernsey                                     | GG   |
| Ghana                                        | GH   |
| Gibraltar                                    | GI   |
| Greenland                                    | GL   |
| Gambia                                       | GM   |
| Guinea                                       | GN   |
| Guadeloupe                                   | GP   |
| Equatorial Guinea                            | GQ   |
| Greece                                       | GR   |
| South Georgia and the South Sandwich Islands | GS   |
| Guatemala                                    | GT   |
| Guam                                         | GU   |
| Guinea-Bissau                                | GW   |
| Guyana                                       | GY   |
| Hong Kong                                    | HK   |
| Heard Island and McDonald Islands            | HM   |
| Honduras                                     | HN   |
| Croatia                                      | HR   |
| Haiti                                        | HT   |
| Hungary                                      | HU   |
| Indonesia                                    | ID   |
| Ireland                                      | IE   |
| Israel                                       | IL   |
| Isle of Man                                  | IM   |
| India                                        | IN   |
| British Indian Ocean Territory               | IO   |
| Iraq                                         | IQ   |
| Iran, Islamic Republic of                    | IR   |
| Iceland                                      | IS   |
| Italy                                        | IT   |
| Jersey                                       | JE   |
| Jamaica                                      | JM   |
| Jordan                                       | JO   |
| Japan                                        | JP   |
| Kenya                                        | KE   |
| Kyrgyzstan                                   | KG   |
| Cambodia                                     | KH   |
| Kiribati                                     | KI   |
| Comoros                                      | KM   |
| Saint Kitts and Nevis                        | KN   |
| Korea, Democratic People's Republic of       | KP   |
| Korea, Republic of                           | KR   |
| Kuwait                                       | KW   |
| Cayman Islands                               | KY   |
| Kazakhstan                                   | KZ   |
| Lao People's Democratic Republic             | LA   |
| Lebanon                                      | LB   |
| Saint Lucia                                  | LC   |
| Liechtenstein                                | LI   |
| Sri Lanka                                    | LK   |
| Liberia                                      | LR   |
| Lesotho                                      | LS   |
| Lithuania                                    | LT   |
| Luxembourg                                   | LU   |
| Latvia                                       | LV   |
| Libyan Arab Jamahiriya                       | LY   |
| Morocco                                      | MA   |
| Monaco                                       | MC   |
| Moldova, Republic of                         | MD   |
| Montenegro                                   | ME   |
| Saint Martin                                 | MF   |
| Madagascar                                   | MG   |
| Marshall Islands                             | MH   |
| Macedonia                                    | MK   |
| Mali                                         | ML   |
| Myanmar                                      | MM   |
| Mongolia                                     | MN   |
| Macao                                        | MO   |
| Northern Mariana Islands                     | MP   |
| Martinique                                   | MQ   |
| Mauritania                                   | MR   |
| Montserrat                                   | MS   |
| Malta                                        | MT   |
| Mauritius                                    | MU   |
| Maldives                                     | MV   |
| Malawi                                       | MW   |
| Mexico                                       | MX   |
| Malaysia                                     | MY   |
| Mozambique                                   | MZ   |
| Namibia                                      | NA   |
| New Caledonia                                | NC   |
| Niger                                        | NE   |
| Norfolk Island                               | NF   |
| Nigeria                                      | NG   |
| Nicaragua                                    | NI   |
| Netherlands                                  | NL   |
| Norway                                       | NO   |
| Nepal                                        | NP   |
| Nauru                                        | NR   |
| Niue                                         | NU   |
| New Zealand                                  | NZ   |
| Oman                                         | OM   |
| Panama                                       | PA   |
| Peru                                         | PE   |
| French Polynesia                             | PF   |
| Papua New Guinea                             | PG   |
| Philippines                                  | PH   |
| Pakistan                                     | PK   |
| Poland                                       | PL   |
| Saint Pierre and Miquelon                    | PM   |
| Pitcairn                                     | PN   |
| Puerto Rico                                  | PR   |
| Palestinian Territory                        | PS   |
| Portugal                                     | PT   |
| Palau                                        | PW   |
| Paraguay                                     | PY   |
| Qatar                                        | QA   |
| Reunion                                      | RE   |
| Romania                                      | RO   |
| Serbia                                       | RS   |
| Russian Federation                           | RU   |
| Rwanda                                       | RW   |
| Saudi Arabia                                 | SA   |
| Solomon Islands                              | SB   |
| Seychelles                                   | SC   |
| Sudan                                        | SD   |
| Sweden                                       | SE   |
| Singapore                                    | SG   |
| Saint Helena                                 | SH   |
| Slovenia                                     | SI   |
| Svalbard and Jan Mayen                       | SJ   |
| Slovakia                                     | SK   |
| Sierra Leone                                 | SL   |
| San Marino                                   | SM   |
| Senegal                                      | SN   |
| Somalia                                      | SO   |
| Suriname                                     | SR   |
| South Sudan                                  | SS   |
| Sao Tome and Principe                        | ST   |
| El Salvador                                  | SV   |
| Sint Maarten                                 | SX   |
| Syrian Arab Republic                         | SY   |
| Swaziland                                    | SZ   |
| Turks and Caicos Islands                     | TC   |
| Chad                                         | TD   |
| French Southern Territories                  | TF   |
| Togo                                         | TG   |
| Thailand                                     | TH   |
| Tajikistan                                   | TJ   |
| Tokelau                                      | TK   |
| Timor-Leste                                  | TL   |
| Turkmenistan                                 | TM   |
| Tunisia                                      | TN   |
| Tonga                                        | TO   |
| Turkey                                       | TR   |
| Trinidad and Tobago                          | TT   |
| Tuvalu                                       | TV   |
| Taiwan                                       | TW   |
| Tanzania, United Republic of                 | TZ   |
| Ukraine                                      | UA   |
| Uganda                                       | UG   |
| United States Minor Outlying Islands         | UM   |
| United States                                | US   |
| Uruguay                                      | UY   |
| Uzbekistan                                   | UZ   |
| Holy See (Vatican City State)                | VA   |
| Saint Vincent and the Grenadines             | VC   |
| Venezuela                                    | VE   |
| Virgin Islands, British                      | VG   |
| Virgin Islands, U.S.                         | VI   |
| Vietnam                                      | VN   |
| Vanuatu                                      | VU   |
| Wallis and Futuna                            | WF   |
| Samoa                                        | WS   |
| Yemen                                        | YE   |
| Mayotte                                      | YT   |
| South Africa                                 | ZA   |
| Zambia                                       | ZM   |
| Zimbabwe                                     | ZW   |

#### multiple-aws-account-values

- **Usage:** Used when one or more AWS Account IDs are required.
- **UI:** List of text fields accepting AWS Account IDs (12 digits)

_Example:_

```json5
{
  id: "S3-015",
  //...
  extraSettings: [
    {
      type: "multiple-aws-account-values",
      name: "friendlyAccounts",
      values: [
        {
          value: "123456789012"
        },
        {
          value: "111111111111"
        }
      ]
    }
  ]
  //...
}
```

#### multiple-ip-values

- **Usage:** Used when one or more IP addresses or CIDRs are required.
- **UI:** List of text fields accepting IP address or CIDRs.

_Example:_

```json5
{
  id: "RTM-007",
  //...
  extraSettings: [
    {
      type: "multiple-ip-values",
      name: "authorisedIps",
      values: [
        {
          value: "1.2.3.4"
        },
        {
          value: "195.200.0.0/24"
        }
      ]
    }
    //...
  ]
  //...
}
```

#### multiple-number-values

- **Usage:** Used when a one or more numbers are required.
- **UI:** List of text fields accepting numbers

_Example:_

```json5
{
  id: "EC2-034",
  //...
  extraSettings: [
    {
      name: "commonlyUsedPorts",
      type: "multiple-number-values",
      values: [
        {
          value: 80
        },
        {
          value: 443
        }
        //...
      ]
    }
  ]
  //...
}
```

#### regions

- **Usage:** Used when one or more AWS region should be selected.
- **UI:** List of on/off sliders for every supported AWS region

Note that setting values only include selected region identifiers.

_Example:_

```json5
{
  id: "RTM-008",
  //...
  extraSettings: [
    {
      type: "regions",
      name: "authorisedRegions",
      values: ["us-east-1", "us-west-2", "ap-southeast-2", "eu-west-1"],
      regions: true
    }
    //...
  ]
  //...
}
```

#### single-number-value

- **Usage:** Used when a single numeric value is required.
- **UI:** Text field accepting numbers

_Example:_

```json5
{
  id: "SQS-003",
  //...
  extraSettings: [
    {
      name: "threshold",
      type: "single-number-value",
      value: 100
    }
  ]
  //...
}
```

#### single-string-value

- **Usage:** Used when a single string value is required.
- **UI:** Text field

_Example:_

```json5
{
  id: "IAM-047",
  //...
  extraSettings: [
    {
      name: "iam_master_role_name",
      type: "single-string-value",
      value: "MasterIAMRole"
    }
    //...
  ]
  //...
}
```

#### single-value-regex

- **Usage:** Used when a regular expression is required.
- **UI:** Text field accepting regular expressions

_Example:_

```json5
{
  id: "VPC-004",
  //...
  extraSettings: [
    {
      name: "pattern",
      type: "single-value-regex",
      value: "^vpc-(ue1|uw1|uw2|ew1|ec1|an1|an2|as1|as2|se1)-(d|t|s|p)-([a-z0-9\\-]+)$"
    }
  ]
  //...
}
```

#### ttl

- **Usage:** Real-time monitoring (RTM) rules have _Time To Live_. This is the
  number of hours that an RTM check remains valid after which time it is expired
  and may get triggered again.
- **UI:** Text field accepting numbers

_Example:_

```json5
{
  id: "RTM-001",
  //...
  extraSettings: [
    {
      name: "ttl",
      type: "ttl",
      value: 2
    }
  ]
  //...
}
```

#### multiple-vpc-gateway-mappings

- **Usage:** Used when one or more VPC gateway mappings are required.
- **UI:** List of VPC Id and Gateway Id mapping

_Example:_

```json5
{
  id: "VPC-013",
  //...
  extraSettings: [
    {
      type: "multiple-vpc-gateway-mappings",
      name: "SpecificVPCToSpecificGatewayMapping",
      mappings: [
        {
          values: [
            {
              type: "single-string-value",
              name: "vpcId",
              value: "vpc-001"
            },
            {
              type: "multiple-string-values",
              name: "gatewayIds",
              values: [
                {
                  value: "nat-001"
                },
                {
                  value: "nat-002"
                }
              ]
            }
          ]
        }
        //...
      ]
    }
  ]
  //...
}
```
