# Standardized Decentralized Service System(SDSS)
We dare to challenge the Cloud Computing cause of censorshiped by the power.
## Why?

So many business services are the core of the blockchain, but where is the value alignment? We say we want build a human digital future.
But it is nothing different with original cloud services: censorshiped by the power.
So we launched this: SDSS proposal and the first product: Rain Computing to explore another way for the future.

## How?
We use ENS and the text record to update all register's domain or ip table with services. Permissionless for all registers with different service registered for V0.1.

## Architecture

**Decentralized Service Discovery and Registration:** This mechanism
   underpins the dynamic operation of the SDSS:
   - **ENS Registry for Service Discovery:** Leverages the Ethereum Name Service
     (ENS) for human-readable naming (e.g., `node.ethpaymaster.eth`) and robust
     service endpoint resolution. Nodes register API endpoints and metadata
     within ENS records, creating a decentralized alternative to centralized
     registries.
   - **Node Registration Mechanism:** Provides a secure, potentially
     pseudonymous (via blockchain address) on-chain registry. Nodes register
     their service capabilities, API endpoints (linked via ENS), and public
     keys. This process may involve staking collateral (e.g., into a
     SuperPaymaster contract) to ensure accountability and security.
   - **Dynamic Routing and Discovery:** Client applications (N0 or dApps)
     dynamically locate suitable API service nodes by querying the ENS-based
     registry (e.g., `api.aastar.eth`) or through client-side cached lists. This
     enables self-maintenance of service records, facilitates failover, and
     allows for node selection based on criteria such as reputation or network
     proximity.

```mermaid
flowchart LR
    subgraph SDSS_DePIN [Standardized Decentralized Service System SDSS - DePIN]
        direction TB

        SDK[SDK] --> N0["N0: Client Node (Tauri+Node.js)"]

        subgraph Service_Discovery_Registration [Decentralized Service Discovery & Registration]
            direction TB
            ENS["ENS Registry (Human-Readable Names & Endpoint Resolution)"]
            OCR["On-Chain Node Registry (Capabilities, API Endpoints via ENS, Public Keys, Staking)"]

            N1_SRV["N1: Static Files & ENS API"] -- Registers --> OCR
            N2_SRV["N2: TEE & Hardware Wallet (ARM/RPi5)"] -- Registers --> OCR
            N3_SRV["N3: Dockerized Services (e.g., Supabase)"] -- Registers --> OCR

            OCR -- Utilizes --> ENS
        end

        N0 -- Accesses Services via --> DYN_ROUTE["Dynamic Routing & Discovery"]
        DYN_ROUTE -- Queries --> ENS
        DYN_ROUTE -- May Use --> CCL["Client-Side Cached Lists"]

        DYN_ROUTE -- Leads to Selection of --> N1_SRV
        DYN_ROUTE -- Leads to Selection of --> N2_SRV
        DYN_ROUTE -- Leads to Selection of --> N3_SRV

        note_permissionless["Anyone can run N0, N1, N2, or N3 nodes (Self-service or Provision)"]
        N0 -.-> note_permissionless
        N1_SRV -.-> note_permissionless
        N2_SRV -.-> note_permissionless
        N3_SRV -.-> note_permissionless

    end
```


## Components

1. CometENS: including frontend for register and management, and a onchain contract, a relay service to resolve ENS.
    https://github.com/AAStarCommunity/CometENS-frontend
    https://github.com/AAStarCommunity/CometENS-Core/tree/aastar-dev
2. Node Register: a node register service for permissionless register to provide any service.
    https://github.com/AAStarCommunity/nodeRegistry
3. SDSS protocol: A standard service invoke protocol, protocol and data structure.
    https://github.com/AAStarCommunity/SDSS , (this repo)

## SDSS V0.1

### API interface standard
1. Restful API
2. URL，请求参数，返回值，状态码，错误码，错误信息，错误码列表，完全遵守HTTP/1.1
3. 新增路径发行协议
    1. 依赖SDSS维护者，提供免费且可转移所有权的ENS域名，以此为基础，提供路径发行的机制。
    2. 对于AAStar维护的机制，我们提供发行paymaster.aastar.eth，发现所有服务者和调用配置。
    3. 服务提供者无许可的进行服务注册（使用我们提供的开源服务和自检、注册工具）
4. 新增多路调用机制（为防止DDos，需要支付token）
5. 原有的Restful API，单独调用依然有效
6. 新增 Reputation 系统，用于评估服务提供者和调用者的成功率，提供不同的权限  

### ENS text record standard

### Onchain node register standard

### Standard invoking flow

## Demo
We create a simple demo for SDSS(Rain Computing) on gas payment senarios.
1. Register a node in node registry.
2. Clone a service repo and run, like a single validator or run your own paymaster service with community token.
3. Submit your service with standard data structure:
  ```json
{
    "name": "AAstar SuperPaymaster Config Demo",
    "version": "SDSS V0.1",
    "description": "A decentralized gas sponsor provider node",
    "image": "https://aastar.io/superpaymaster.png",
    "url": "https://aastar.io/superpaymaster",
    "ens": "paymaster.aastar.eth",
    "address": "0x1234567890123456789012345678901234567890",
    "stake": {
        "eth": "1000",
        "aastar": "1000",
        "promise": {
            "duration": "30d",
            "amount": "1000",
            "item": "url/ipfs",
            "token-accept": {
                "eth": "0x0000000000000000000000000000000000000000",
                "astPNTs": "0x1234567890123456789012345678901234567890",
                "USDT": "0x1234567890123456789012345678901234567890",
                "USDC": "0x1234567890123456789012345678901234567890",
                "DAI": "0x1234567890123456789012345678901234567890",
                "WETH": "0x1234567890123456789012345678901234567890"
            },
            "price": {
                "eth": "30",
                "astPNTs": "30",
                "USDT": "30",
                "USDC": "30",
                "DAI": "30",
                "WETH": "30"
            }
        }
    },
    "openpnts": {
        "factory": "0x1234567890123456789012345678901234567890",
        "PNTs": "0x1234567890123456789012345678901234567890",
        "ratio": "ratio.aastar.eth",
        "symbol": "astPNTs"
    },
    "opencards": {
        "factory": "0x1234567890123456789012345678901234567890",
        "nft": "0x1234567890123456789012345678901234567890",
        "ratio": "ratio.aastar.eth",
        "symbol": "astCards"
    },
    "Paymaster config": {
        "token-accept": [{
            "symbol": "astPNTs",
            "address": "0x1234567890123456789012345678901234567890",
            "price": "30"
        }, {
            "symbol": "xPNTs",
            "address": "0x0000000000000000000000000000000000000000",
            "price": "20"
        }],
        "limitation": {
            "daily": "1000",
            "single": "1 ETH"
        }
    }
}

```


