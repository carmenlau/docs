---
description: The app configuration authgear.yaml
---

# authgear.yaml

This is the main configuration file affecting every aspect of Authgear.

## JSON Schema

The configuration file is validated against the following JSON Schema:

```javascript
{
  "$defs": {
    "AppConfig": {
      "additionalProperties": false,
      "properties": {
        "authentication": {
          "$ref": "#/$defs/AuthenticationConfig"
        },
        "authenticator": {
          "$ref": "#/$defs/AuthenticatorConfig"
        },
        "database": {
          "$ref": "#/$defs/DatabaseConfig"
        },
        "forgot_password": {
          "$ref": "#/$defs/ForgotPasswordConfig"
        },
        "hook": {
          "$ref": "#/$defs/HookConfig"
        },
        "http": {
          "$ref": "#/$defs/HTTPConfig"
        },
        "id": {
          "type": "string"
        },
        "identity": {
          "$ref": "#/$defs/IdentityConfig"
        },
        "localization": {
          "$ref": "#/$defs/LocalizationConfig"
        },
        "messaging": {
          "$ref": "#/$defs/MessagingConfig"
        },
        "metadata": {
          "$ref": "#/$defs/AppMetadata"
        },
        "oauth": {
          "$ref": "#/$defs/OAuthConfig"
        },
        "redis": {
          "$ref": "#/$defs/RedisConfig"
        },
        "session": {
          "$ref": "#/$defs/SessionConfig"
        },
        "template": {
          "$ref": "#/$defs/TemplateConfig"
        },
        "ui": {
          "$ref": "#/$defs/UIConfig"
        },
        "verification": {
          "$ref": "#/$defs/VerificationConfig"
        },
        "welcome_message": {
          "$ref": "#/$defs/WelcomeMessageConfig"
        }
      },
      "required": [
        "id"
      ],
      "type": "object"
    },
    "AppMetadata": {
      "additionalProperties": false,
      "patternProperties": {
        "^app_name(#.+)?$": {
          "type": "string"
        },
        "^logo_uri(#.+)?$": {
          "format": "uri",
          "type": "string"
        }
      },
      "type": "object"
    },
    "AuthenticationConfig": {
      "additionalProperties": false,
      "properties": {
        "device_token": {
          "$ref": "#/$defs/DeviceTokenConfig"
        },
        "identities": {
          "items": {
            "$ref": "#/$defs/IdentityType"
          },
          "type": "array",
          "uniqueItems": true
        },
        "primary_authenticators": {
          "items": {
            "$ref": "#/$defs/PrimaryAuthenticatorType"
          },
          "type": "array",
          "uniqueItems": true
        },
        "recovery_code": {
          "$ref": "#/$defs/RecoveryCodeConfig"
        },
        "secondary_authentication_mode": {
          "$ref": "#/$defs/SecondaryAuthenticationMode"
        },
        "secondary_authenticators": {
          "items": {
            "$ref": "#/$defs/SecondaryAuthenticatorType"
          },
          "type": "array",
          "uniqueItems": true
        }
      },
      "type": "object"
    },
    "AuthenticatorConfig": {
      "additionalProperties": false,
      "properties": {
        "oob_otp": {
          "$ref": "#/$defs/AuthenticatorOOBConfig"
        },
        "password": {
          "$ref": "#/$defs/AuthenticatorPasswordConfig"
        },
        "totp": {
          "$ref": "#/$defs/AuthenticatorTOTPConfig"
        }
      },
      "type": "object"
    },
    "AuthenticatorOOBConfig": {
      "additionalProperties": false,
      "properties": {
        "email": {
          "$ref": "#/$defs/AuthenticatorOOBEmailConfig"
        },
        "sms": {
          "$ref": "#/$defs/AuthenticatorOOBSMSConfig"
        }
      },
      "type": "object"
    },
    "AuthenticatorOOBEmailConfig": {
      "additionalProperties": false,
      "properties": {
        "code_digits": {
          "maximum": 8,
          "minimum": 4,
          "type": "integer"
        },
        "maximum": {
          "type": "integer"
        },
        "message": {
          "$ref": "#/$defs/EmailMessageConfig"
        }
      },
      "type": "object"
    },
    "AuthenticatorOOBSMSConfig": {
      "additionalProperties": false,
      "properties": {
        "code_digits": {
          "maximum": 8,
          "minimum": 4,
          "type": "integer"
        },
        "maximum": {
          "type": "integer"
        },
        "message": {
          "$ref": "#/$defs/SMSMessageConfig"
        }
      },
      "type": "object"
    },
    "AuthenticatorPasswordConfig": {
      "additionalProperties": false,
      "properties": {
        "policy": {
          "$ref": "#/$defs/PasswordPolicyConfig"
        }
      },
      "type": "object"
    },
    "AuthenticatorTOTPConfig": {
      "additionalProperties": false,
      "properties": {
        "maximum": {
          "type": "integer"
        }
      },
      "type": "object"
    },
    "DatabaseConfig": {
      "additionalProperties": false,
      "properties": {
        "max_connection_lifetime_seconds": {
          "minimum": 0,
          "type": "integer"
        },
        "max_idle_connection": {
          "minimum": 0,
          "type": "integer"
        },
        "max_open_connection": {
          "minimum": 0,
          "type": "integer"
        }
      },
      "type": "object"
    },
    "DeviceTokenConfig": {
      "additionalProperties": false,
      "properties": {
        "disabled": {
          "type": "boolean"
        },
        "expire_in_days": {
          "$ref": "#/$defs/DurationDays"
        }
      },
      "type": "object"
    },
    "DurationDays": {
      "type": "integer"
    },
    "DurationSeconds": {
      "type": "integer"
    },
    "EmailMessageConfig": {
      "additionalProperties": false,
      "patternProperties": {
        "^reply_to(#.+)?$": {
          "format": "email-name-addr",
          "type": "string"
        },
        "^sender(#.+)?$": {
          "format": "email-name-addr",
          "type": "string"
        },
        "^subject(#.+)?$": {
          "type": "string"
        }
      },
      "type": "object"
    },
    "ForgotPasswordConfig": {
      "additionalProperties": false,
      "properties": {
        "email_message": {
          "$ref": "#/$defs/EmailMessageConfig"
        },
        "enabled": {
          "type": "boolean"
        },
        "reset_code_expiry_seconds": {
          "$ref": "#/$defs/DurationSeconds"
        },
        "sms_message": {
          "$ref": "#/$defs/SMSMessageConfig"
        }
      },
      "type": "object"
    },
    "HTTPConfig": {
      "additionalProperties": false,
      "properties": {
        "allowed_origins": {
          "items": {
            "type": "string"
          },
          "type": "array"
        },
        "hosts": {
          "items": {
            "type": "string"
          },
          "type": "array"
        }
      },
      "type": "object"
    },
    "HookConfig": {
      "additionalProperties": false,
      "properties": {
        "handlers": {
          "items": {
            "$ref": "#/$defs/HookHandlerConfig"
          },
          "type": "array"
        },
        "sync_hook_timeout_seconds": {
          "$ref": "#/$defs/DurationSeconds"
        },
        "sync_hook_total_timeout_seconds": {
          "$ref": "#/$defs/DurationSeconds"
        }
      },
      "type": "object"
    },
    "HookHandlerConfig": {
      "additionalProperties": false,
      "properties": {
        "event": {
          "type": "string"
        },
        "url": {
          "format": "uri",
          "type": "string"
        }
      },
      "required": [
        "event",
        "url"
      ],
      "type": "object"
    },
    "IdentityConfig": {
      "additionalProperties": false,
      "properties": {
        "login_id": {
          "$ref": "#/$defs/LoginIDConfig"
        },
        "oauth": {
          "$ref": "#/$defs/OAuthSSOConfig"
        },
        "on_conflict": {
          "$ref": "#/$defs/IdentityConflictConfig"
        }
      },
      "type": "object"
    },
    "IdentityConflictConfig": {
      "additionalProperties": false,
      "properties": {
        "promotion": {
          "$ref": "#/$defs/PromotionConflictBehavior"
        }
      },
      "type": "object"
    },
    "IdentityType": {
      "enum": [
        "login_id",
        "oauth",
        "anonymous"
      ],
      "type": "string"
    },
    "LocalizationConfig": {
      "additionalProperties": false,
      "properties": {
        "fallback_language": {
          "type": "string"
        }
      },
      "type": "object"
    },
    "LoginIDConfig": {
      "additionalProperties": false,
      "properties": {
        "keys": {
          "items": {
            "$ref": "#/$defs/LoginIDKeyConfig"
          },
          "type": "array"
        },
        "types": {
          "$ref": "#/$defs/LoginIDTypesConfig"
        }
      },
      "type": "object"
    },
    "LoginIDEmailConfig": {
      "additionalProperties": false,
      "properties": {
        "block_plus_sign": {
          "type": "boolean"
        },
        "case_sensitive": {
          "type": "boolean"
        },
        "ignore_dot_sign": {
          "type": "boolean"
        }
      },
      "type": "object"
    },
    "LoginIDKeyConfig": {
      "additionalProperties": false,
      "properties": {
        "key": {
          "type": "string"
        },
        "maximum": {
          "type": "integer"
        },
        "type": {
          "$ref": "#/$defs/LoginIDKeyType"
        },
        "verification": {
          "$ref": "#/$defs/VerificationLoginIDKeyConfig"
        }
      },
      "required": [
        "key",
        "type"
      ],
      "type": "object"
    },
    "LoginIDKeyType": {
      "enum": [
        "raw",
        "email",
        "phone",
        "username"
      ],
      "type": "string"
    },
    "LoginIDTypesConfig": {
      "additionalProperties": false,
      "properties": {
        "email": {
          "$ref": "#/$defs/LoginIDEmailConfig"
        },
        "username": {
          "$ref": "#/$defs/LoginIDUsernameConfig"
        }
      },
      "type": "object"
    },
    "LoginIDUsernameConfig": {
      "additionalProperties": false,
      "properties": {
        "ascii_only": {
          "type": "boolean"
        },
        "block_reserved_usernames": {
          "type": "boolean"
        },
        "case_sensitive": {
          "type": "boolean"
        },
        "excluded_keywords": {
          "items": {
            "type": "string"
          },
          "type": "array"
        }
      },
      "type": "object"
    },
    "MessagingConfig": {
      "additionalProperties": false,
      "properties": {
        "default_email_message": {
          "$ref": "#/$defs/EmailMessageConfig"
        },
        "default_sms_message": {
          "$ref": "#/$defs/SMSMessageConfig"
        },
        "sms_provider": {
          "$ref": "#/$defs/SMSProvider"
        }
      },
      "type": "object"
    },
    "OAuthClientConfig": {
      "additionalProperties": false,
      "properties": {
        "access_token_lifetime_seconds": {
          "$ref": "#/$defs/DurationSeconds"
        },
        "client_id": {
          "type": "string"
        },
        "client_uri": {
          "format": "uri",
          "type": "string"
        },
        "grant_types": {
          "items": {
            "type": "string"
          },
          "type": "array"
        },
        "post_logout_redirect_uris": {
          "items": {
            "format": "uri",
            "type": "string"
          },
          "type": "array"
        },
        "redirect_uris": {
          "items": {
            "format": "uri",
            "type": "string"
          },
          "minItems": 1,
          "type": "array"
        },
        "refresh_token_lifetime_seconds": {
          "$ref": "#/$defs/DurationSeconds"
        },
        "response_types": {
          "items": {
            "type": "string"
          },
          "type": "array"
        }
      },
      "required": [
        "client_id",
        "redirect_uris"
      ],
      "type": "object"
    },
    "OAuthConfig": {
      "additionalProperties": false,
      "properties": {
        "clients": {
          "items": {
            "$ref": "#/$defs/OAuthClientConfig"
          },
          "type": "array"
        }
      },
      "type": "object"
    },
    "OAuthSSOConfig": {
      "additionalProperties": false,
      "properties": {
        "providers": {
          "items": {
            "$ref": "#/$defs/OAuthSSOProviderConfig"
          },
          "type": "array"
        }
      },
      "type": "object"
    },
    "OAuthSSOProviderConfig": {
      "additionalProperties": false,
      "properties": {
        "alias": {
          "type": "string"
        },
        "client_id": {
          "type": "string"
        },
        "key_id": {
          "type": "string"
        },
        "team_id": {
          "type": "string"
        },
        "tenant": {
          "type": "string"
        },
        "type": {
          "$ref": "#/$defs/OAuthSSOProviderType"
        }
      },
      "required": [
        "type",
        "client_id"
      ],
      "type": "object"
    },
    "OAuthSSOProviderType": {
      "enum": [
        "google",
        "facebook",
        "linkedin",
        "azureadv2",
        "apple"
      ],
      "type": "string"
    },
    "PasswordPolicyConfig": {
      "additionalProperties": false,
      "properties": {
        "digit_required": {
          "type": "boolean"
        },
        "excluded_keywords": {
          "items": {
            "type": "string"
          },
          "type": "array"
        },
        "history_days": {
          "$ref": "#/$defs/DurationDays"
        },
        "history_size": {
          "type": "integer"
        },
        "lowercase_required": {
          "type": "boolean"
        },
        "min_length": {
          "type": "integer"
        },
        "minimum_guessable_level": {
          "type": "integer"
        },
        "symbol_required": {
          "type": "boolean"
        },
        "uppercase_required": {
          "type": "boolean"
        }
      },
      "type": "object"
    },
    "PrimaryAuthenticatorType": {
      "enum": [
        "password",
        "oob_otp"
      ],
      "type": "string"
    },
    "PromotionConflictBehavior": {
      "enum": [
        "error",
        "login"
      ],
      "type": "string"
    },
    "RecoveryCodeConfig": {
      "additionalProperties": false,
      "properties": {
        "count": {
          "type": "integer"
        },
        "list_enabled": {
          "type": "boolean"
        }
      },
      "type": "object"
    },
    "RedisConfig": {
      "additionalProperties": false,
      "properties": {
        "idle_connection_timeout_seconds": {
          "minimum": 0,
          "type": "integer"
        },
        "max_connection_lifetime_seconds": {
          "minimum": 0,
          "type": "integer"
        },
        "max_idle_connection": {
          "minimum": 0,
          "type": "integer"
        },
        "max_open_connection": {
          "minimum": 0,
          "type": "integer"
        }
      },
      "type": "object"
    },
    "SMSMessageConfig": {
      "additionalProperties": false,
      "properties": {
        "^sender(#.+)?$": {
          "format": "phone",
          "type": "string"
        }
      },
      "type": "object"
    },
    "SMSProvider": {
      "enum": [
        "nexmo",
        "twilio"
      ],
      "type": "string"
    },
    "SecondaryAuthenticationMode": {
      "enum": [
        "if_requested",
        "if_exists",
        "required"
      ],
      "type": "string"
    },
    "SecondaryAuthenticatorType": {
      "enum": [
        "password",
        "oob_otp",
        "totp"
      ],
      "type": "string"
    },
    "SessionConfig": {
      "additionalProperties": false,
      "properties": {
        "cookie_domain": {
          "type": "string"
        },
        "cookie_non_persistent": {
          "type": "boolean"
        },
        "idle_timeout_enabled": {
          "type": "boolean"
        },
        "idle_timeout_seconds": {
          "$ref": "#/$defs/DurationSeconds"
        },
        "lifetime_seconds": {
          "$ref": "#/$defs/DurationSeconds"
        }
      },
      "type": "object"
    },
    "TemplateConfig": {
      "additionalProperties": false,
      "properties": {
        "items": {
          "items": {
            "$ref": "#/$defs/TemplateItem"
          },
          "type": "array"
        }
      },
      "type": "object"
    },
    "TemplateItem": {
      "additionalProperties": false,
      "properties": {
        "language_tag": {
          "type": "string"
        },
        "type": {
          "$ref": "#/$defs/TemplateItemType"
        },
        "uri": {
          "type": "string"
        }
      },
      "required": [
        "type",
        "uri"
      ],
      "type": "object"
    },
    "TemplateItemType": {
      "type": "string"
    },
    "UIConfig": {
      "additionalProperties": false,
      "properties": {
        "country_calling_code": {
          "$ref": "#/$defs/UICountryCallingCodeConfig"
        },
        "custom_css": {
          "type": "string"
        }
      },
      "type": "object"
    },
    "UICountryCallingCodeConfig": {
      "additionalProperties": false,
      "properties": {
        "default": {
          "type": "string"
        },
        "values": {
          "items": {
            "type": "string"
          },
          "type": "array"
        }
      },
      "type": "object"
    },
    "VerificationConfig": {
      "additionalProperties": false,
      "properties": {
        "code_expiry_seconds": {
          "$ref": "#/$defs/DurationSeconds"
        },
        "criteria": {
          "$ref": "#/$defs/VerificationCriteria"
        },
        "email": {
          "$ref": "#/$defs/VerificationEmailConfig"
        },
        "sms": {
          "$ref": "#/$defs/VerificationSMSConfig"
        }
      },
      "type": "object"
    },
    "VerificationCriteria": {
      "enum": [
        "any",
        "all"
      ],
      "type": "string"
    },
    "VerificationEmailConfig": {
      "additionalProperties": false,
      "properties": {
        "message": {
          "$ref": "#/$defs/EmailMessageConfig"
        }
      },
      "type": "object"
    },
    "VerificationLoginIDKeyConfig": {
      "additionalProperties": false,
      "properties": {
        "enabled": {
          "type": "boolean"
        },
        "required": {
          "type": "boolean"
        }
      },
      "type": "object"
    },
    "VerificationSMSConfig": {
      "additionalProperties": false,
      "properties": {
        "message": {
          "$ref": "#/$defs/SMSMessageConfig"
        }
      },
      "type": "object"
    },
    "WelcomeMessageConfig": {
      "additionalProperties": false,
      "properties": {
        "destination": {
          "$ref": "#/$defs/WelcomeMessageDestination"
        },
        "email_message": {
          "$ref": "#/$defs/EmailMessageConfig"
        },
        "enabled": {
          "type": "boolean"
        }
      },
      "type": "object"
    },
    "WelcomeMessageDestination": {
      "enum": [
        "first",
        "all"
      ],
      "type": "string"
    }
  },
  "$ref": "#/$defs/AppConfig"
}
```

## Annotated example

```yaml
# The ID of this instance of Authgear.
id: myapp
# Configure different identity behavior.
identity:
  login_id:
    # Defines the set of accepted login IDs.
    # The configuration shown here is the default.
    # So by default the user can have
    #
    # At most 1 email
    # At most 1 phone
    # At most 1 username
    #
    # If you do not want the defaults, define keys yourselves.
    keys:
      # Define the key of the login ID.
    - key: email
      # Define the type of login ID.
      # Valid values are "email" "phone" "username" and "raw"
      type: email
      # How many login ID the user can have.
      # Default is 1.
      maximum: 1
      # Configure verification of this login ID key.
      verification:
        # Whether verification is enabled for this login ID key, default to true for email & phone type
        enabled: true
        # Whether verification is required for this login ID key, default to true for email & phone type.
        required: false
    - key: phone
      type: phone
    - key: username
      type: username
    # Configure the characteristics of some login IDs.
    types:
      # Configure Email Login ID Identity.
      email:
        # Whether + sign should be disallowed in the local part. Default is false.
        block_plus_sign: false
        # Whether the email should be treated case sensitively. Default is false.
        case_sensitive: false
        # Whether . sign should be ignored. Default is false.
        ignore_dot_sign: false
      # Configure Username Login ID Identity.
      username:
        # Whether the username can only contain `-a-zA-Z0-9_.`. Default is true.
        ascii_only: true
        # Whether reserved usernames are blocked. Default is true.
        block_reserved_usernames: true
        # Whether the username should be treated case sensitively. Default is false.
        case_sensitive: false
        # Define a list of banned usernames. Default is empty list.
        excluded_keywords:
        - admin
  # Configure OAuth Identity.
  oauth:
    # Configure external OAuth identity providers.
    providers:
    # Denote the type of the identity provider.
    # Valid values are "google", "apple", "facebook", "azureadv2", "linkedin"
    - type: google
      # alias by default is the same as the value of the type.
      alias: google
      # Client ID and client secret are the credentials you obtain from the specific provider.
      # Please refer to the documentation of the provider.
      # You must separately provide the client secret in the secret config file.
      client_id: google_client_id
    - type: apple
      alias: apple
      # The client ID for Apple is the services ID.
      # The client secret for Apple is the PEM format of the private key.
      client_id: apple_services_id
      # The key ID of the private key.
      key_id: key_id
      # The team ID of your Apple Developer Account.
      team_id: team_id
    - type: azureadv2
      alias: azure
      client_id: client_id
      # Tenant is either the special value "common", the special value "organizations" or
      # the ID of a Azure AD tenant.
      #
      # Note that when you create the client in Azure Portal,
      # you have to choose which tenant the client intends to interact with.
      #
      # If you wish to allow any microsoft accounts such as
      #
      # - hotmail
      # - Xbox
      # - Outlook
      #
      # to login, then the value must be "common".
      #
      # If you wish to allow any user in any Azure ADs in your Azure account,
      # then the value must be "organizations".
      #
      # Otherwise the value must be the ID of a Azure AD tenant.
      # In this case, only user in that Azure AD can login.
      tenant: common
  on_conflict:
    # Configure the behavior in anonymous user promotion when the claimed identity
    # conflicts with an existing identity.
    #
    # Valid values are "error" and "login".
    # Default is "error".
    #
    # For example, the user initially signed up as "user@example.com".
    # Later on the user uninstalled the mobile app.
    # The user installed the mobile app again and forgot they had signed up before.
    # The user continued as anonymous user.
    # The user finally opted to sign up with "user@example.com".
    # At this point, the user has 2 accounts.
    #
    # If the value is "error", an error is shown telling the user that
    # the identity they are claiming has been claimed by another user.
    #
    # If the value is "login", the anonymous user is discarded.
    # And the user simply authenticates themselves as the original user.
    # It is up to the developer to handle account merging.
    promotion: "error"
  # Configure Login ID Identity.
# Configure different authenticator behavior.
authenticator:
  # Configure OOB-OTP Authenticator.
  oob_otp:
    email:
      # the maximum number of the authenticator the user can have.
      # default is 1.
      maximum: 1
      # message is EmailMessageConfig
      message:
        reply_to: no-reply@example.com
        sender: System <system@example.com>
        subject: Verify your email
      # the number of digits in the OTP, default to 6.
      code_digits: 4
    sms:
      # the maximum number of the authenticator the user can have.
      # default is 1.
      maximum: 1
      # message is SMSMessageConfig
      message:
       sender: +85299887766
      # the number of digits in the OTP, default to 6.
      code_digits: 4
  # Configure Password Authenticator
  password:
    # Configure password policy
    # All policies are turned off by default.
    policy:
      # Set the minimum length of new password.
      min_length: 10
      # Require new password to have at least 1 digit.
      digit_required: true
      # Require new password to have at least 1 lowercase ASCII character.
      lowercase_required: true
      # Require new password to have at least 1 uppercase ASCII character.
      uppercase_required: true
      # Require new password to have at least 1 symbol character.
      symbol_required: true
      # Disallow password containing the given keywords.
      excluded_keywords:
      - secret
      - admin
      - password
      # Require strong password.
      # The strength of the password is calculated with https://github.com/dropbox/zxcvbn
      # 1 is the weakest level and 5 is the strongest level.
      minimum_guessable_level: 5
      # Determine how long password history is kept.
      history_days: 90
      # Determine how many password history is kept.
      history_size: 10
  # Configure TOTP Authenticator
  totp:
    # the maximum number of the authenticator the user can have.
    # default is 1.
    maximum: 1
# Configure the authentication behavior.
authentication:
  # Determine which identities are enabled.
  # By default "login_id" and "oauth" are enabled.
  identities:
  - login_id
  - oauth
  - anonymous
  # Determine which authenticators can be used as primary authenticator.
  # By default only "password" is enabled.
  primary_authenticators:
  - password
  - oob_otp
  # Determine which authenticators can be used as secondary authenticator.
  # By default totp, oob_otp are enabled.
  secondary_authenticators:
  - password
  - totp
  - oob_otp
  # Configure the MFA behavior.
  #
  # if_exists: The user can add secondary authenticators.
  # If the user has at least one secondary authenticator, then MFA must be performed.
  #
  # required: The user must add secondary authenticators.
  # The user must perform MFA during authentication.
  #
  # if_requested: MFA is entirely optional even the user has at least one secondary authenticator.
  #
  # Default is "if_exists"
  secondary_authentication_mode: if_exists
  # Configure Device Token.
  # Device token can be generated during MFA.
  # It is used to skip MFA on the device for future authentication.
  device_token:
    # Determine how long the device token is valid.
    expire_in_days: 30
  # Configure Recovery Code
  recovery_code:
    # The number of recovery codes. Default is 16.
    count: 16
    # Whether the user can list the recovery codes again. Default is false.
    list_enabled: false
# Configure forgot password behavior
forgot_password:
  # How long the reset code remains valid. The default is 1200. That is 20 minutes.
  reset_code_expiry_seconds: 1200
  # email_message is EmailMessageConfig
  email_message: {}
  # sms_message is SMSMessageConfig
  sms_message: {}
# Configure webhook
hook:
  # How long a single handler can proceed the webhook event before timeout.
  # Default is 5.
  sync_hook_timeout_seconds: 5
  # How long all handlers can proceed the webhook event before timeout.
  # Default is 10.
  sync_hook_total_timeout_seconds: 10
  # Define the list of webhook handlers
  handlers:
    # The event name.
  - event: before_user_create
    # The endpoint of the webhook handler.
    url: https://api.example.com/hook/before_user_create
http:
  # The allowed origin for the HTTP header access-control-allow-origin
  # Default is empty list.
  allowed_origins:
  - https://trusted-third-party-server.com
  # The expected host
  # Default is empty list.
  hosts:
  - https://accounts.myapp.com
# Configure default messaging configuration.
messaging:
  # Configure default email message configuration.
  # default_email_message is EmailMessageConfig.
  default_email_message:
    reply_to: no-reply@example.com
    sender: info@example.com
    subject: App
  # Configure default SMS configuration.
  # default_sms_message is SMSMessageConfig.
  default_sms_message:
    sender: "+85299887766"
  # Configure which SMS provider to use.
  # Valid values are "twilio" and "nexmo".
  # You must provide the credentials in secret config.
  sms_provider: "twilio"
# Configure the database connection
database:
  # The maximum open connection to the database.
  # The default is 2.
  max_open_connection: 2
  # The maximum idle connection to the database.
  # The default is 2.
  max_idle_connection: 2
  # The maximum lifetime of the connection.
  # The connection is discarded when its lifetime reaches the value.
  # The default is 1800.
  max_connection_lifetime_seconds: 1800
# Configure Redis connection
redis:
  # The maximum open connection to Redis.
  # The default is 2.
  max_open_connection: 2
  # The maximum idle connection to Redis.
  # The default is 2.
  max_idle_connection: 2
  # The maximum lifetime of the connection.
  # The connection is discarded when its lifetime reaches the value.
  # The default is 900.
  max_connection_lifetime_seconds: 900
  # Idle connections are closed after remaining idle for this duration.
  # The default is 300.
  idle_connection_timeout_seconds: 300
# Configure user verification
verification:
  # Determine the verification status criteria.
  # any: User is verified if any of the verifiable identities is verified
  # all: User is verified if all of the verifiable identities are verified
  # Default to any.
  criteria: any
  # Lifetime of verification code, default to 3600 (1 hour)
  code_expiry_seconds: 3600
  # Configure verification SMS message
  sms:
    message:
       sender: +85299887766
  # Configure verification email message
  email:
    message:
      reply_to: no-reply@example.com
      sender: System <system@example.com>
      subject: Verify your email
# Configure localization.
localization:
  # The fallback language when none of the supported languages match the preferred languages.
  # Default is en.
  fallback_language: en
# Configure the metadata of Authgear.
metadata:
  # Set the user-facing app name.
  # It is shown in the web UI.
  app_name: My App
  app_name#ja-JP: アプリ
  # Set the logo URI in the web UI.
  logo_uri: https://static.example.com/logo.png
# Configure OAuth.
oauth:
  # Define the list of known OAuth 2 clients.
  clients:
    # The OAuth 2 client ID.
    # A reasonably long secure random string is recommended.
  - client_id: client_id
    # Define a list of allowed redirect URIs.
    # According to OAuth 2 spec, exact match is used.
    # So "http://example.com" does not match "http://example.com/"
    redirect_uris:
    - "com.myapp://host/path"
    # Which grant types are allowed in the token endpoint.
    # "authorization_code" and "refresh_token" must be included for OAuth 2 authorization code flow.
    grant_types:
    - authorization_code
    - refresh_token
    # What response the authorization endpoint can return.
    # "code" must be included for OAuth 2 authorization code flow.
    response_types:
    - code
    # Define a list of allowed post logout redirect URIs.
    # Same as redirect_uris, exact match is used.
    post_logout_redirect_uris:
    - "https://www.myapp.com/post_logout"
    # The lifetime of the access token. Default is 1800.
    access_token_lifetime_seconds: 1800
    # The lifetime of the refresh token. Default is 86400.
    refresh_token_lifetime_seconds: 86400
# Configure session.
session:
  # Explicitly set the cookie domain. Default is eTLD+1.
  cookie_domain: https://accounts.myapp.com
  # Whether the cookie is session cookie. Default is false.
  cookie_non_persistent: false
  # Whether the session becomes invalid after idling.
  idle_timeout_enabled: false
  # How long before the session timeout.
  idle_timeout_seconds: 300
  # The lifetime of the session. Default is 86400.
  lifetime_seconds: 86400
# Configure template.
template:
  # Override default templates or provide additional translation files.
  items:
    # The type of template.
  - type: auth_ui_translation.json
    # The language of the template file.
    language_tag: ja-JP
    # The URI to load the template.
    # Only file scheme is supported.
    uri: file:///app/templates/auth_ui_transation.ja.json
ui:
  # Define a custom inline stylesheet to be injected in every pages of the UI.
  custom_css: |
    .a { color: red; }
  country_calling_code:
    # The default selected value of the country calling code.
    # Default is the first item in values.
    default: 852
    # The list of country calling code to show in the phone number input widget.
    values:
    - 852
# Configure welcome message.
welcome_message:
  # Whether to send the welcome message.
  # Default is false.
  enabled: false
  # Whether to send the welcome message to all addresses or first address.
  # Valid values are first and all.
  # Default is first.
  destination: first
  # email_message is EmailMessageConfig.
  email_message: {}
```
