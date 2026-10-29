# AssetClaw Security Policy

This policy covers the AssetClaw project:

- **The website** at [assetclaw.xyz](https://assetclaw.xyz) (home and the Genesis 625 page) and the app at [app.assetclaw.xyz](https://app.assetclaw.xyz): the bridge (RWA Native, Privacy and Standard), claims and history.
- **The AssetClaw backend** that prepares bridge quotes and claims and reports volume.
- **The AssetClaw Telegram bot** ([@assetclawbot](https://t.me/assetclawbot)) and its wallet, trading and monitoring service.

The only official websites are **assetclaw.xyz** and **app.assetclaw.xyz**. AssetClaw never sends the first direct message, and never asks for a seed phrase or private key.

## Reporting a vulnerability

Please report security issues privately. **Do not open a public issue.**

- Email: assetclawofficial@gmail.com
- Or contact an admin through the official channels listed on assetclaw.xyz

Please include:

- a description of the issue and its possible impact;
- steps to reproduce, if possible;
- any relevant addresses, transaction hashes or logs.

We aim to acknowledge reports promptly and will keep you updated on the fix. We credit reporters who wish to be acknowledged.

## Your wallet and keys

- **Website: non-custodial.** You connect your own wallet and sign every transaction yourself. AssetClaw never holds your keys or your funds.
- **Telegram bot:** the bot creates a wallet for you. You can export the key at any time, protected by your export password, and use it in any standard wallet. You are never locked in.

## Website and backend

**Every transaction is checked before your wallet opens.** For RWA Native bridging and claims, the website keeps its own list of the official Asset Chain bridge contracts and the AssetClaw treasury. Each approval, deposit, fee and claim prepared by our backend must match that list:

- the right bridge for the chain and token;
- the funds going to your own wallet on the destination chain;
- the fee going to the AssetClaw treasury, at no more than 1%.

If anything does not match, the website stops with a safety message and never asks your wallet to sign.

**Claims and statistics are verified on-chain.** A claim is reported to Asset Chain only after the backend confirms on-chain that it really happened. Bridge volume is only counted after the transaction is checked on-chain.

**Browser protections.** The website cannot be loaded inside another site (protection against clickjacking), is served only over HTTPS, and sends standard security headers. A content security policy is being introduced in monitoring mode, so its rules are proven before they are enforced.

**Phishing protection.** Every page reminds visitors that the only official sites are assetclaw.xyz and app.assetclaw.xyz.

**Secrets.** API keys, database credentials and signing credentials stay on the server, in environment configuration. They are never committed to source control or sent to the browser, and error messages never include internal details.

**Abuse limits.** Public endpoints are rate-limited per visitor, with tighter limits on those that use partner credentials. Admin endpoints require a key and are switched off when unset.

**Dependencies.** Packages are locked to exact, verified versions, including the SilentSwap SDK that builds Privacy and Standard swaps. Updates are reviewed and tested before release.

## Telegram bot

**Wallet key protection.** Private keys are encrypted at rest with authenticated encryption (AES-256-GCM), using a separate derived key per user. Keys are decrypted only in memory, at the moment a transaction is signed, and are never stored or logged in plain text.

**Transaction safety.** Swaps go only through a fixed, trusted on-chain router. Slippage is capped (0.5%, 1% or 3%), every trade enforces a minimum output, and every transaction carries a short deadline so it cannot be executed late.

**Input validation.** Addresses and amounts are validated before use, and wallet actions only ever apply to the requesting user's own account.

**Secrets.** The master encryption key and other secrets live in environment configuration, never in source control or logs.

## Third parties

AssetClaw builds on infrastructure we do not control. We cannot guarantee their security or availability:

- **Asset Chain:** the RWA Native bridge contracts and the bridge orchestrator that signs claims.
- **SilentSwap:** routing for Privacy and Standard swaps. Approvals and in-transit funds follow SilentSwap's own design. SilentSwap has published security audits by [Halborn](https://www.halborn.com/audits/silentswap/v2---cps--gateway-3179a0), [Hacken](https://hacken.io/audits/silentswap/) and [CertiK](https://skynet.certik.com/projects/silent-swap).
- **Wallets, blockchain RPC providers, decentralized exchanges and price sources.**
- **Token contracts.** A token's contract is written by its own creators and may behave maliciously regardless of our safeguards. Always do your own research before trading a token.

## Reviews

We run regular internal security reviews of the website, backend and bot, covering transaction building and signing, wallet handling, access control, secrets and endpoints. The latest internal review was completed on 28 October 2026, and its findings were fixed or tracked before the Genesis 625 launch.

This document describes our practices. It is not a warranty, and it is not a substitute for a formal third-party audit. Trading and bridging digital assets carries risk, including total loss.
