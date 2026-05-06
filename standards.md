# Standards & API Reference

> Project: Loyalty & Rewards Platform · Generated: 2026-05-03

## Industry Standards & Specifications

### ISO Standards

**ISO 20022 — Financial Messaging Standard**
- URL: https://www.iso20022.org/iso-20022
- Relevance: The global standard for financial data interchange, covering payment initiation, settlement, and cash reporting. Relevant when a loyalty platform supports monetary redemption of points (cash-back, gift cards, bank transfer payouts) or integrates with payment rails for linked-card earning. ISO 20022 messages carry richer remittance data than older formats, enabling more precise attribution of loyalty triggers to specific transactions.

**ISO/IEC 27001 — Information Security Management Systems**
- URL: https://www.iso.org/standard/27001
- Relevance: The de facto enterprise security certification for SaaS platforms. Loyalty platforms handle sensitive personal data (purchase history, behavioral profiles, payment-linked identifiers) that enterprise retail customers expect to be protected under ISO 27001-certified environments. SOC 2 Type II certification is the US-market equivalent also expected by enterprise buyers.

**ISO/IEC 29100 — Privacy Framework**
- URL: https://www.iso.org/standard/45123.html
- Relevance: Provides a high-level privacy framework that supports GDPR and CCPA compliance implementation. Relevant for loyalty platforms that collect and process behavioral, preference, and transactional personal data for personalisation and segmentation, establishing principles for consent, purpose limitation, and data minimisation.

### W3C & IETF Standards

**RFC 6749 — OAuth 2.0 Authorization Framework**
- URL: https://datatracker.ietf.org/doc/html/rfc6749
- Relevance: The authentication foundation for all loyalty platform partner integrations: e-commerce platforms (Shopify, BigCommerce), CRM systems, email/SMS providers, POS systems, and coalition partner networks. Loyalty platforms must implement OAuth 2.0 to obtain and refresh credentials on behalf of merchants and to expose partner APIs securely within coalition ecosystems.

**RFC 6750 — OAuth 2.0 Bearer Token Usage**
- URL: https://datatracker.ietf.org/doc/html/rfc6750
- Relevance: Defines how OAuth access tokens are transmitted in API requests. Required for all loyalty API integrations with e-commerce and marketing platforms.

**OpenID Connect Core 1.0 — Identity Layer over OAuth 2.0**
- URL: https://openid.net/specs/openid-connect-core-1_0.html
- Relevance: Enables SSO between a loyalty platform and partner merchant ecosystems, coalition partner portals, and enterprise customer identity systems. Members should be able to log in to any partner in a coalition using a single identity, enabling seamless cross-brand loyalty experiences without requiring separate account creation.

**RFC 7231 — HTTP/1.1 Semantics and Content**
- URL: https://datatracker.ietf.org/doc/html/rfc7231
- Relevance: Defines HTTP method semantics and status codes for all loyalty REST API integrations. Critical for correct idempotency handling in points-award and redemption API calls (which must be exactly-once to prevent double-awarding or double-redemption).

**RFC 7807 — Problem Details for HTTP APIs**
- URL: https://datatracker.ietf.org/doc/html/rfc7807
- Relevance: Standardises structured error payloads from REST APIs. Loyalty platforms should adopt this for their own APIs to enable integration partners to build deterministic error-handling for failed point awards, invalid redemption attempts, and tier change events.

**RFC 8288 — Web Linking**
- URL: https://datatracker.ietf.org/doc/html/rfc8288
- Relevance: Provides the standard for linking related resources in HTTP responses (e.g. linking a member record to their transaction history, reward catalogue, or tier status). Supports HATEOAS-style API design for headless loyalty engines.

### Data Model & API Specifications

**OpenAPI Specification 3.1 (OAS 3.1)**
- URL: https://spec.openapis.org/oas/v3.1.0.html
- Relevance: The industry standard for documenting REST APIs. Antavo, Open Loyalty, Talon.One, Voucherify, Zinrelo, LoyaltyLion, and Yotpo all expose APIs documented in OpenAPI/Swagger format. A loyalty platform should publish its own OAS 3.1 specification to enable integration partner SDK generation, contract testing, and automated documentation.

**JSON Schema 2020-12**
- URL: https://json-schema.org/specification
- Relevance: Standard for validating JSON payloads. Used to validate member profile data, point transaction records, reward redemption events, gamification challenge definitions, and campaign rule payloads in loyalty platform APIs. Critical for preventing data quality issues that corrupt point balances or tier calculations.

**GS1 Digital Link — Product-Level Loyalty Triggers via 2D Barcodes**
- URL: https://www.gs1.org/standards/gs1-digital-link
- Relevance: GS1 Digital Link enables a 2D QR code or barcode to function as both a point-of-sale scanner and a web-based product URL. This enables physical retail loyalty integrations where scanning a product barcode in-store can trigger loyalty point awards, product-level promotions, or personalised offers — without requiring a dedicated loyalty app. GS1 has set a Sunrise Date of 2027 for full retail adoption of Digital Link as a successor to UPC barcodes.

**Webhook / CloudEvents Specification**
- URL: https://cloudevents.io (CNCF)
- Relevance: CloudEvents is a CNCF specification for standardising the schema and delivery of event notifications via webhooks. Loyalty platforms must publish events (member enrolment, point award, redemption, tier change, challenge completion) to integration partners via webhooks. Adopting CloudEvents ensures a consistent, interoperable event schema across all loyalty event types.

### Security & Compliance Standards

**PCI DSS v4.0 — Payment Card Industry Data Security Standard**
- URL: https://www.pcisecuritystandards.org/standards/
- Relevance: Required for loyalty platforms that implement linked-card earning (where points are awarded based on payment card transactions at any merchant), store card tokens for recurring billing of paid loyalty memberships (Amazon Prime-style), or otherwise store, process, or transmit payment card data. Even platforms using tokenisation must understand PCI DSS v4.0 requirements for token scope and data minimisation.

**GDPR — General Data Protection Regulation (EU 2016/679)**
- URL: https://gdpr.eu/
- Relevance: Loyalty platforms are specifically scrutinised under GDPR because they collect highly sensitive behavioural and purchasing profiles used for personalisation. EU members must be able to request erasure, data portability, and restriction of processing. Loyalty platforms must maintain a lawful basis for each data processing activity and provide clear privacy notices explaining how purchase history is used for reward personalisation. Data Processing Agreements are required with all integrated platforms (CRM, email, SMS providers).

**CCPA / CPRA — California Consumer Privacy Act (and Regulations)**
- URL: https://oag.ca.gov/privacy/ccpa
- Relevance: California's Attorney General has specifically targeted loyalty programs as a CCPA enforcement priority. Loyalty programs collecting personal data in exchange for rewards are classified as "financial incentive programs" under CCPA, requiring a Notice of Financial Incentive explaining the value exchange, opt-in consent, and an opt-out mechanism. Participation must be voluntary and cannot restrict access to unrelated products.

**OWASP API Security Top 10 (2023)**
- URL: https://owasp.org/API-Security/editions/2023/en/0x11-t10/
- Relevance: Defines the ten most critical API security risks. For loyalty platforms, the most relevant are: Broken Object-Level Authorization (each member may only access their own point balance and reward history); Broken Authentication (loyalty tokens must be properly scoped); Unrestricted Access to Sensitive Business Flows (point-award and redemption endpoints are high-value fraud targets requiring rate limiting and anti-abuse controls); and Broken Object Property Level Authorization (preventing unauthorised tier manipulation or points injection via mass assignment vulnerabilities).

### MCP Server Specifications

**Model Context Protocol (MCP) — Agentic Loyalty Personalisation**
- URL: https://modelcontextprotocol.io/ ; https://www.arcweb.com/blog/ai-supply-chain-part-3-mcp-model-context-protocol-shared-reasoning-across-agents
- Relevance: MCP is the emerging standard for connecting AI agents to external tools. In the loyalty context, Google has announced MCP-based integrations enabling AI shopping agents to discover products, apply loyalty rewards, and personalise experiences in a single conversation flow. Retail AI agents powered by Claude, Gemini, or ChatGPT can use MCP tool calls to query a member's point balance, available rewards, and redemption eligibility — then apply loyalty discounts mid-purchase without requiring the member to navigate a separate loyalty portal. Loyalty platforms should plan MCP server exposure to support agentic commerce workflows becoming mainstream in 2026–2027.

---

## Similar Products — Developer Documentation & APIs

### Open Loyalty

- **Description:** MIT-licensed, API-first headless loyalty engine. The open-source core provides maximum flexibility for custom-built loyalty programmes covering points, tiers, gamification, campaigns, and member management. Available as self-hosted or managed cloud SaaS.
- **API Documentation:** https://apidocs.openloyalty.io/ ; https://docs.openloyalty.io/en/latest/api/index.html
- **Developer Portal:** https://www.openloyalty.io/role/developers
- **SDKs/Libraries:** REST API with Postman collections; no official language-specific SDK (headless/custom integration model)
- **Standards:** REST/JSON; JWT authentication; OpenAPI/Swagger documentation; fully headless (no default frontend)
- **Authentication:** JWT tokens (auto-generated documentation built in)
- **Licence:** MIT (open-source core); commercial SaaS available

### Antavo Loyalty Management Platform

- **Description:** Pure-play enterprise loyalty SaaS covering points, tiers, gamification, coalition rewards, and omnichannel campaigns with a REST API and SDKs for custom integrations.
- **API Documentation:** https://apidocs.antavo.com/
- **Developer Portal:** https://antavo.com/developers
- **SDKs/Libraries:** PHP SDK — https://github.com/antavo/loyalty-sdk-php
- **Standards:** REST/JSON; OpenAPI-documented endpoints; events submitted via Events API; Display API for customer-specific UIs
- **Authentication:** API Key + API Secret (region-scoped); per-merchant credentials

### Talon.One Promotion & Loyalty Engine

- **Description:** API-first promotion and loyalty engine for rule-based campaigns, coupons, referrals, and loyalty programs. Strong promotion logic with a no-code rule builder and real-time campaign evaluation API.
- **API Documentation:** https://docs.talon.one/integration-api
- **Developer Portal:** https://www.talon.one/developers
- **SDKs/Libraries:** PHP SDK — https://github.com/talon-one/TalonOnePHPsdk ; C# SDK — https://github.com/talon-one/TalonOne.cs ; additional SDKs per developer portal
- **Standards:** REST/JSON; OpenAPI specification published; real-time integration via Integration API and Management API
- **Authentication:** API Key

### Voucherify — Incentive Optimisation Engine

- **Description:** API-first promotions and loyalty engine covering coupons, gift cards, referrals, and loyalty programs. TypeScript-first SDK, OpenAPI-generated client libraries, and REST API with predictable resource-oriented design.
- **API Documentation:** https://docs.voucherify.io/reference/introduction-1
- **Developer Guide:** https://docs.voucherify.io/docs/welcome
- **SDKs/Libraries:** JavaScript/TypeScript SDK — https://github.com/voucherifyio/voucherify-js-sdk (npm: @voucherify/sdk)
- **Standards:** REST/JSON; OpenAPI 3.0 specification (SDK auto-generated by OpenAPI Generator); API version v2018-08-01
- **Authentication:** Application ID + Application Secret Key (header-based)

### Salesforce Loyalty Management

- **Description:** Enterprise loyalty management built on Salesforce CRM, covering member management, program rules, tiers, rewards catalogue, partner programmes, and member communications. Integrated with Salesforce Marketing Cloud and Data Cloud.
- **API Documentation:** https://developer.salesforce.com/docs/atlas.en-us.loyalty.meta/loyalty/loyalty_management_apis.htm
- **REST Reference:** https://developer.salesforce.com/docs/atlas.en-us.loyalty.meta/loyalty/loyalty_management_apis_rest_references.htm
- **Developer Guide (Spring '26):** https://resources.docs.salesforce.com/latest/latest/en-us/sfdc/pdf/loyalty_api.pdf
- **Standards:** REST/JSON; Salesforce platform APIs; standard Salesforce data model (LoyaltyProgram, LoyaltyProgramMember objects)
- **Authentication:** OAuth 2.0 (Salesforce Connected Apps)

### Yotpo Loyalty

- **Description:** E-commerce-focused loyalty platform with Shopify-native integration. Covers points, referrals, VIP tiers, and SMS integrations. Separate loyalty API for custom headless integrations.
- **API Documentation:** https://loyaltyapi.yotpo.com/reference/welcome ; https://apidocs.yotpo.com/reference
- **App Developer API:** https://develop.yotpo.com/reference
- **Support Docs:** https://support.yotpo.com/docs/api-and-integrations
- **Standards:** REST/JSON; OpenAPI-style documentation; Postman collections available
- **Authentication:** API Key + GUID (merchant-scoped)

### LoyaltyLion

- **Description:** Data-driven loyalty platform for e-commerce brands with a Headless API enabling custom UIs for headless storefronts. OpenAPI-specified endpoints with a TypeScript client library.
- **API Documentation:** https://developers.loyaltylion.com/
- **Headless API:** https://developers.loyaltylion.com/headless-api/introduction
- **SDKs/Libraries:** TypeScript Headless API Client — https://github.com/loyaltylion/typescript-headless-api-client
- **Standards:** REST/JSON; OpenAPI specification (TypeScript client fully typed from OpenAPI spec); headless architecture
- **Authentication:** API Key (site_id in path); OAuth for headless API endpoints

### Smile.io

- **Description:** SMB-focused loyalty platform for Shopify and BigCommerce brands. REST API available on Plus and Enterprise plans for custom extensions, custom earning actions, and integration with third-party tools.
- **API Documentation:** https://help.smile.io/en/articles/4036313-smile-api-overview
- **GitHub:** https://github.com/smile-io
- **Standards:** REST/JSON; API explorer built into documentation
- **Authentication:** API Key (scoped per key; multiple keys with fine-grained permissions)
- **Note:** API access restricted to Plus/Enterprise plans; Shopify or BigCommerce required as ecommerce platform.

### Zinrelo

- **Description:** AI/ML-powered loyalty platform for mid-to-large enterprises with REST API for custom integrations, webhook support for CRM and email system connectivity, and analytics-focused data exports.
- **API Documentation:** https://zinrelo.github.io/slate/ ; https://help.zinrelo.com/reference/introduction
- **Standards:** REST/JSON; Slate-formatted API reference; webhook event delivery for member events
- **Authentication:** Partner ID + API Key (HTTP header per request)
- **SDK Note:** Language bindings documented in Shell and Python

### Capillary Technologies (Loyalty+)

- **Description:** AI-driven enterprise loyalty and CRM platform, dominant in Asia-Pacific markets, covering omnichannel personalisation, tiered programs, gamification, and coalition partner management. Deep integration with Adobe Experience Platform and MoEngage.
- **API Documentation:** https://docs.capillarytech.com/
- **Standards:** REST/JSON; plug-and-play API connectors; Adobe Real-Time CDP native integration
- **Authentication:** API credentials per merchant deployment; OAuth-compatible for partner ecosystem integrations

### Currency Alliance — Loyalty API Network

- **Description:** Currency Alliance provides a loyalty technology layer enabling multi-partner loyalty ecosystems — allowing points to be earned, transferred, and redeemed across partner networks via a standardised API. Relevant for coalition and interoperability use cases.
- **API Documentation:** https://www.currencyalliance.com/insights/loyalty-technology-for-the-api-economy
- **Standards:** REST API; partnership-based API agreements between loyalty programme operators
- **Authentication:** Partner API credentials; merchant-specific tokens

---

## Notes

**Loyalty API Interoperability Gap (2026):** Unlike payments (ISO 20022) or e-commerce (OpenAPI-documented marketplace APIs), loyalty programmes have no dominant open interoperability standard. Currency Alliance and Loyyal Network are working to address this gap with partner API networks and (as of April 2026) an alpha interoperable loyalty infrastructure platform respectively. This remains an underserved area — an open-source loyalty platform exposing a well-documented OpenAPI 3.1 spec could serve as a de facto integration standard for coalition ecosystems.

**GS1 Digital Link Sunrise 2027:** The retail industry transition to GS1 Digital Link 2D barcodes as a successor to UPC (Sunrise 2027) creates a significant opportunity for loyalty platforms: product-level loyalty triggers via scannable QR codes without requiring a dedicated loyalty app install. Loyalty platforms should track this transition and plan barcode-triggered earning integrations.

**CCPA Enforcement Priority:** The California Attorney General has specifically identified loyalty programme data practices as a priority enforcement area. Loyalty platforms must implement CCPA-compliant financial incentive notices, consent management, and opt-out workflows from the outset — not as an afterthought.

**Fraud Risk in Loyalty APIs:** Point-award and redemption API endpoints are high-value fraud targets. Loyalty platforms must implement idempotency keys (exactly-once semantics), rate limiting per member and per integration partner, anomaly detection for abnormal earning patterns, and audit logs for all balance modifications. These are not covered by any published standard but are critical operational requirements.
