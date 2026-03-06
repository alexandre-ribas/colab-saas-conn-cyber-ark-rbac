# colab-saas-conn-cyberark-rbac

[![Discourse Topics](https://img.shields.io/discourse/topics?label=Discuss%20This%20Tool&server=https%3A%2F%2Fdeveloper.sailpoint.com%2Fdiscuss)](https://developer.sailpoint.com/discuss/tag/workflows)
[![Issues](https://img.shields.io/github/issues/sailpoint-oss/repo-template?label=Issues)](https://github.com/sailpoint-oss/repo-template/issues)
[![Latest Releases](https://img.shields.io/github/v/release/sailpoint-oss/repo-template?label=Current%20Release)](https://github.com/sailpoint-oss/repo-template/releases)
[![Contributor Shield](https://img.shields.io/github/contributors/sailpoint-oss/repo-template?label=Contributors)](https://github.com/sailpoint-oss/repo-template/graphs/contributors)

## Overview

A SailPoint SaaS Connector designed to integrate with **CyberArk Privilege Cloud** utilizing **RBAC** (Role-Based Access Control). It manages accounts, groups, safe roles, and safe rights, providing a seamless identity governance experience between SailPoint Identity Security Cloud and CyberArk Privilege Cloud.

**Supported Operations:**
* Account Management: `create`, `enable`, `disable`, `update`, `read`, `list`
* Entitlement Management: `list` (Groups, Safe Roles, Safe Rights)
* Test Connection

## Prerequisites

Before using or developing this connector, ensure you have the following requirements met:
* **Node.js** (v18 or higher recommended)
* **npm** (Node Package Manager)
* **SailPoint CLI** (`spcx` or `sail`) installed and configured with your tenant.
* Authorized administrative access to a **CyberArk Privilege Cloud** environment.
* CyberArk Identity Application configured with standard OAuth2 Client Credentials for API consumption.

## Configuration & Environment Variables

This connector requires the following configuration parameters (usually configured via the SailPoint UI after deployment, or defined within a local `config.json` for local development):

| Configuration Key      | Type     | Description                                                                                     | Required |
|------------------------|----------|-------------------------------------------------------------------------------------------------|----------|
| `identityTenantUrl`    | URL      | CyberArk Identity Tenant URL.                                                                   | Yes      |
| `clientId`             | String   | OAuth2 Client ID from CyberArk Identity.                                                        | Yes      |
| `clientSecret`         | Secret   | OAuth2 Client Secret.                                                                           | Yes      |
| `oauthAppId`           | String   | Default OAuth Application Name/ID.                                                              | Yes      |
| `oauthScope`           | String   | Space-separated list of scopes required for API access.                                         | Yes      |
| `safeRoles`            | Textarea | List or mapping of Safe Roles available.                                                        | Yes      |
| `safeRights`           | Textarea | List or mapping of Safe Rights available.                                                       | Yes      |
| `accountSource`        | Enum     | Source of the account (`activeDirectory` or `cyberArk`).                                        | Yes      |
| `directoryServiceId`   | String   | Required if `accountSource` is set to `activeDirectory`.                                        | Optional |
| `ignoreSSL`            | Boolean  | Ignore SSL certificate errors (useful for self-signed certificates or test environments).       | No       |

## Running Locally

To run and test the connector locally on your machine:

1. **Install dependencies**:
   ```bash
   npm install
   ```

2. **Create a local mock configuration**:
   Create a `config.json` file in the root of the project with your test credentials matching the configuration keys from `connector-spec.json`.

3. **Run local development mode**:
   ```bash
   npm run dev
   ```
   *Note: This utilizes the `spcx` CLI to run the connector locally, listening securely for commands from the SailPoint platform.*

4. **Run Unit Tests**:
   To run unit tests and ensure functionality works as expected:
   ```bash
   npm run test
   ```

## Deployment to SailPoint Platform

To deploy the connector to your SailPoint Identity Security Cloud tenant:

1. **Build and package the connector**:
   This compiles the TypeScript code and produces a deployable ZIP file, packaging all dependencies securely.
   ```bash
   npm run pack-zip
   ```
   *Note: This command runs `npm ci && npm run build`*

2. **Deploy via SailPoint CLI**:
   Create a new connector in your tenant:
   ```bash
   sail connectors create "CyberArk Privilege Cloud RBAC"
   ```
   To upload a new packed version of the connector:
   ```bash
   sail connectors upload -c <Connector-ID> -f <path-to-generated-zip-file>
   ```

---

## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag `enhancement`.
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See `LICENSE.txt` for more information.
