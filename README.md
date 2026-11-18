
![Whisk_b3eb88c403](https://github.com/user-attachments/assets/ebea4ee4-8fd4-4d52-ba94-8004a2e12581)

<div align="center">

# Hella Main Web Site 

[![Deployment](https://github.com/hella-web3/hella-site-base/actions/workflows/jekyll.yml/badge.svg)](https://github.com/hella-web3/hella-site-base/actions/workflows/jekyll.yml)

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://github.com/codespaces/new?repo=hella-web3/hella-site-base)

Base website for [Hella](https://hellalabs.dev).  Built with Jekyll and barebones pure CSS/Sass and Javascript.

</div>

---

## 🚀 Overview

**Hella Site Base** is a web3-focused website showcasing our expertise in performance, security, and developer experience.

We are active contributors to the Ethereum ecosystem, maintaining open-source projects that set the standard for Web3 test automation and developer tooling:
- **[Foundry Anvil Testcontainers Nodejs](https://github.com/hella-web3/foundryanvil-testcontainers-nodejs)**: High-fidelity Anvil node orchestration for Node.js E2E tests.
- **[Wiremock Testcontainers Nodejs](https://github.com/hella-web3/wiremock-testcontainers-nodejs)**: Fluent TypeScript API for WireMock, optimizing test isolation and speed.
- **[Ethereum Transaction Explorer TUI](https://github.com/anataliocs/etherscan-tui-go)**: A developer-centric terminal UI for exploring EVM transactions.

We leverage this deep technical expertise to provide **Fractional Engineering Services** for emerging Web3 startups.

**Tech Stack:**
- Jekyll
- CSS/Sass
- Javascript
- Github Actions
- Devcontainers

And that's it!

---

## 📦 Installation

Config and setup.

**Install rbenv**
```terminaloutput
brew install rbenv
rbenv init
```

**Install ruby**
```terminaloutput
rbenv install 3.4.3
rbenv global 3.4.3
```

**Update bundler**
```terminaloutput
gem install bundler -v 2.6.7
```

---

## 🛠️ Usage

Local dev instructions.

**Run app with live reloading**
```
bundle install && bundle exec jekyll serve --livereload
``` 

Visit [ http://127.0.0.1:4000]( http://127.0.0.1:4000) after starting the server.

---

## 🛠️ Build

GH Actions.

**Run build**
```
gh workflow run jekyll.yml
gh run list --workflow="jekyll.yml"
``` 

Visit [https://hellalabs.dev](https://hellalabs.dev) after the workflow run completes.

---

## 🤝 Contributing

We welcome contributions! Please check our [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## 📄 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## 💬 Social

- Twitter: [@hella_web3](https://twitter.com/hella_web3)
- [LinkedIn](https://www.linkedin.com/company/hella-web3)
- [Youtube](https://www.youtube.com/@hella-web3)
- [Dev.to](https://dev.to/hella-web3)
- [Github](https://github.com/hella-web3)

---

<div align="center">

_Made with ❤️ by the Hella Labs team_

Speeding up the transition to a Web3 future.

Release: 0.0.4

</div>
