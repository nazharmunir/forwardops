# Security notes

ForwardOps is a demonstration application and must not be used for real freight operations.

The prototype intentionally illustrates several controls:

- external text is treated as untrusted data;
- suspicious directives can place a request on security hold;
- required operational fields are validated deterministically;
- execution requires an explicit human action;
- the custom sandbox runs locally in the browser and sends no data to an AI API.

For a production system, use authenticated users, least-privilege service credentials, server-side authorization, secret management, durable audit logging, rate limiting, payload validation, dependency scanning and a formal threat model.

Please do not report real vulnerabilities against third-party freight systems through this repository. This project is independent and contains no third-party credentials or integrations.

## Contact

For security issues that are specific to this demonstration repository, contact **Muhammad Mazhar Munir** at [mazhar.munir1233@gmail.com](mailto:mazhar.munir1233@gmail.com).
