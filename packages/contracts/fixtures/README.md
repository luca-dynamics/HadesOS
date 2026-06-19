# Contract Fixtures

Future fixtures in this directory must be synthetic, deterministic, and privacy-safe. Real user data, real customer data, real access tokens, real file paths containing usernames, real messages, real calendar entries, real device identifiers, and real organization identifiers must never be committed.

Fixtures should be designed to exercise safety-kernel and connector behavior for:

- approved action
- denied action
- expired approval
- revoked connector
- forbidden action
- missing rollback metadata
- scope violation

Use stable fake identifiers, fixed timestamps, synthetic object names, and deliberately minimal payloads so tests remain reproducible across local, cloud, and enterprise implementations.
