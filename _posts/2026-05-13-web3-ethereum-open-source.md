---
layout: post
title: Open-Source Web3 Ethereum Projects at Hella Labs
description: Supporting the Web3 Ethereum ecosystem with open source projects, tools and test automation.
date: 2026-05-13 9:29:35 +0300
image: '/images/blog/github-open-source.png'
tags: [ Ethereum, Javascript, Typescript, Testcontainers, Wiremock, Foundry ]
tags_color: '#4643ec'
featured: true
sitemap: true
---

## Open Source Web3 Ethereum Projects

[Hella Labs](https://github.com/hella-web3) supports several Ethereum open-source projects.  These projects specialize in test automation.

**Projects:**

- [Foundry Anvil Testcontainers Nodejs](https://www.npmjs.com/package/@hellaweb3/foundryanvil-testcontainers-nodejs)
- [Wiremock Testcontainers Nodejs](https://www.npmjs.com/package/@hellaweb3/wiremock-testcontainers-nodejs)
- [Ethereum Transaction Explorer TUI](https://github.com/anataliocs/etherscan-tui-go)

----

## Foundry Anvil Testcontainers Nodejs

This repository provides a [Testcontainers](https://testcontainers.com/) module for Node.js to run a customized Anvil node in your E2E tests.

This Typescript module provides a **Fluent API** style method of configuring and starting the Anvil node, mapping every Anvil flag to a type-safe configuration builder. During your test execution, the module provides a [viem test client](https://viem.sh/docs/clients/test) and streamlined helper methods to interact with the node.

**Key Features:**
- **Full Anvil Flag Support:** Configure everything from mining modes to forking and EVM limits using a type-safe API.
- **State Overrides & Fixtures:** Easily mock dependencies with `setCode`, state overrides, and custom genesis files.
- **Advanced EVM Features:** Support for EIP-712 and EIP-7702 signing, chain reorgs, and call tracing.
- **Improved DX:** Immediate validation of conflicting flags prevents misconfiguration before the container even starts.

- [https://github.com/hella-web3/foundryanvil-testcontainers-nodejs](https://github.com/hella-web3/foundryanvil-testcontainers-nodejs)
- [https://www.npmjs.com/package/@hellaweb3/foundryanvil-testcontainers-nodejs](https://www.npmjs.com/package/@hellaweb3/foundryanvil-testcontainers-nodejs)

<br/>
_Get started with Foundry Anvil Testcontainers Nodejs by following the steps below._

#### Install:
```
pnpm add -D @hellaweb3/foundryanvil-testcontainers-nodejs
```

#### Setup:
```typescript
import { AnvilContainer, AnvilOptions, Hardfork, useAnvil } from "@hellaweb3/foundryanvil-testcontainers-nodejs";
import { parseEther } from "viem";

const options = new AnvilOptions()
    .account.withAccounts(5).withBalance(1_000)
    .evm.withChainId(1337).withHardfork(Hardfork.Cancun)
    .logs.quiet();

// Starts in beforeAll, stops in afterAll, restores the state after every test.
const anvil = useAnvil(
    new AnvilContainer(options).withTestClient((client) => client.withAccount(0)),
);

it("sends Ether", async () => {
    const [, bob] = await anvil.addresses();
    // `account` is optional: the test client has a typed default account.
    const receipt = await anvil.confirm(
        anvil.testClient.sendTransaction({ to: bob, value: parseEther("1") }),
    );
    expect(receipt.status).toBe("success");
    expect(await anvil.testClient.getChainId()).toBe(1337);
});

it("manipulates the chain fluently", async () => {
    const whale = "0x1111111111111111111111111111111111111111";
    await anvil.cheats.setBalanceEther(whale, 1_000).impersonate(whale).increaseTime({ days: 7 }).mine();
});
```

Check out the [docs](https://www.npmjs.com/package/@hellaweb3/foundryanvil-testcontainers-nodejs) for more info.

----

## Wiremock Testcontainers Nodejs

`wiremock-testcontainers-nodejs` is a Typescript nodejs library that spins up a WireMock instance with [Testcontainers](https://testcontainers.com/). 
It provides a fluent API to configure and start WireMock containers, including support for loading mappings and files from recorded [Wiremock](https://wiremock.org/) sessions.

**Key Features:**
- **Flexible Stub Registration:** Serve stubs from directories, files, npm packages, or inline JSON.
- **Test Isolation:** Reset state between tests (`reset()`, `resetRequests()`) without restarting the container, significantly speeding up E2E suites.
- **Verification API:** Verify what your code sent through WireMock's request journal directly from your test suite.
- **Extensibility:** Load WireMock extensions from JARs (no local JDK required) or use TypeScript extensions.
- **No-Docker Mode:** Optional support for running via local JVM for environments without a container runtime.

- [https://github.com/hella-web3/wiremock-testcontainers-nodejs](https://github.com/hella-web3/wiremock-testcontainers-nodejs)
- [https://www.npmjs.com/package/@hellaweb3/wiremock-testcontainers-nodejs](https://www.npmjs.com/package/@hellaweb3/wiremock-testcontainers-nodejs)

<br/>
_Get started with Wiremock Testcontainers Nodejs by following the steps below._

#### Install:
```
pnpm add -D @hellaweb3/wiremock-testcontainers-nodejs testcontainers
```

#### Setup:
```typescript
import { afterAll, afterEach, beforeAll, expect, it } from "vitest"; // or Jest
import { type StartedWiremockContainer, WiremockContainer } from "@hellaweb3/wiremock-testcontainers-nodejs";
import { PaymentsClient } from "../app/payments-client"; // the code under test

let wiremock: StartedWiremockContainer;

beforeAll(async () => {
    wiremock = await new WiremockContainer()
        .withMappings("./__mocks__/wiremock") // mappings/ + __files/
        .start();
    await wiremock.waitUntilReady();
}, 120_000); // the first image pull can be slow

afterEach(() => wiremock.reset()); // pristine stubs, empty journal – no restart
afterAll(() => wiremock?.stop());

it("lists the recorded payments", async () => {
    const page = await new PaymentsClient(wiremock.getUrl()).list();

    expect(page.meta.totalItems).toBe(2);
    expect(await wiremock.countRequests({ method: "GET", url: "/payments" })).toBe(1);
});
```

Check out the [npm repo](https://www.npmjs.com/package/@hellaweb3/wiremock-testcontainers-nodejs) for more info.
Check out the [docs](https://hella-web3.github.io/wiremock-testcontainers-nodejs/) for more info.

----

## Ethereum Transaction Explorer TUI

A terminal(TUI) Ethereum transaction explorer built with Go and the [Bubble Tea](https://github.com/charmbracelet/bubbletea) TUI framework. Fetch, 
display and explore details for any Ethereum transaction hash using the Etherscan API V2 all in your terminal.

**Key Features:**
- **Multi-Network Support:** Seamlessly explore transactions on both Ethereum Mainnet and Sepolia.
- **Rich Terminal UI:** Built with `bubbletea`, `bubbles`, and `lipgloss` for a high-fidelity terminal experience.
- **Real-time Data:** Fetches transaction details, gas prices, and confirmations directly via Etherscan API.
- **Developer-Centric:** Designed for developers who prefer staying in the terminal while debugging smart contract interactions.

[https://github.com/anataliocs/etherscan-tui-go](https://github.com/anataliocs/etherscan-tui-go)

----

## Ethereum Transaction Explorer TUI

A terminal(TUI) Ethereum transaction explorer built with Go and the [Bubble Tea](https://github.com/charmbracelet/bubbletea) TUI framework. Fetch, 
display and explore details for any Ethereum transaction hash using the Etherscan API V2 all in your terminal.

Built with bubbletea, bubbles, and lipgloss.

[https://github.com/anataliocs/etherscan-tui-go](https://github.com/anataliocs/etherscan-tui-go)

----

Help make ethereum more secure with better test automation.

_Thanks for reading and supporting open source. Post your comments below!_

