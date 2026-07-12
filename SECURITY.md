Security Policy — AssetClaw Bot

This policy covers the AssetClaw trading & wallet bot specifically (the Telegram
bot and its wallet, trading, and monitoring backend). It does not cover other parts of
the AssetClaw project such as the website or other services, which are maintained
separately.

AssetClaw is non-custodial. We take the security of user funds and data seriously.
This document explains the bot's security practices at a high level and how to report
a vulnerability responsibly.

Reporting a Vulnerability

If you believe you have found a security vulnerability in the AssetClaw bot, please
report it privately. Do not open a public issue.


Email: assetclawofficial@gmail.com
Or contact an admin directly via our official channels (see assetclaw.xyz)


Please include:


A description of the issue and its potential impact
Steps to reproduce, if possible
Any relevant addresses, transaction hashes, or logs


We aim to acknowledge reports within a reasonable time and will keep you updated on
remediation. We appreciate responsible disclosure and will credit reporters who wish
to be acknowledged.

The Bot's Security Practices

Wallet key protection. Private keys are encrypted at rest using authenticated
encryption (AES-256-GCM) with per-user key derivation. Keys are decrypted only
transiently in memory at the moment a transaction is signed, and are never stored or
logged in plaintext.

Non-custodial by design. Users can export their private key at any time (protected
by a personal export password) to load their wallet into any standard Web3 wallet. You
are never locked in.

Secret handling. Application secrets (API keys, database credentials, the master
encryption key) are held in environment configuration, never committed to source
control, and never written to logs or error messages.

Transaction safety. Swaps route only through a fixed, trusted on-chain router.
Slippage is bounded to a small maximum, and minimum-output protection is enforced on
every trade. Every transaction carries a short deadline to prevent stale execution.

Input validation. All user-supplied addresses and amounts are validated before use.
Wallet operations are scoped to the requesting user's own account.

Dependency hygiene. We monitor the bot's dependencies for known vulnerabilities and
keep them patched.

Ongoing review. We conduct regular internal security reviews of the bot's codebase,
covering wallet handling, transaction logic, access control, and its network endpoints.

Scope and Limitations

This policy applies to the AssetClaw bot only. The bot interacts with third-party
infrastructure (blockchain RPC providers, decentralized exchanges, price sources). We
cannot guarantee the security or availability of external services or of third-party
token contracts. Always do your own research before trading any token — a token's
contract is written by its own creators and may behave maliciously regardless of our
safeguards.

Nothing in this document is a warranty. Trading digital assets carries risk, including
total loss.


This reflects the internal security practices of the AssetClaw bot and is not a
substitute for a formal third-party audit.
