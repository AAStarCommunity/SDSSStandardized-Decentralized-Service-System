# SDSS (Standardized-Decentralized-Service-System) V0.1
Standardized Decentralized Service System, SDSS, proposed by AAStar to improve the business service to decentralized.

## Why?
So many business services are the core of the blockchain, but where is the value alignment? We say we want build a human digital future.
But it is nothing different with original cloud services: censorshiped by the power.
So we launched this: SDSS proposal and the first product: Rain Computing to explore another way for the future.

## How?
We use ENS and the text record to update all register's domain or ip table with services. Permissionless for all registers with different service registered.
The invokers only need know one ENS domain and they can enjoy all services with one request.

## Demo
We create a simple demo for SDSS(Rain Computing) on gas payment senarios.

### Example in SuperPaymaster
1. DApp send a request to paymaster.aastar.eth to get a collection of services
   maintained by AAStar(anyone can use CometENS,SuperPaymaster and more to
   create a service like this in different level)
2. Or DApp send to a single paymaster service like jason.paymaster.aastar.eth
   maintained by AAStar and service provider.
3. You will get a 15 minutes fresh service list or a single service description
   including service provider, support ERC20 tokens, sponsor price, reputation,
   and Web2 domain or IP.
4. Choose the favor price or reputation you like to invoke the service to get
   the gas payment signature and send your transaction to be on-chain.
5. The server side include some service relay (bundler and paymaster service) for specific business target.
6. The service supplier will get the gas payment and deduct the PNTs from your
   AirAccount which pre-approved in creating AirAccount by EIP 777 operator.

### Flow chart


### Defination
1. root ENS domain is a open source organization mark. Like aastar.eth
2. second level is for different services, like paymaster.aastar.eth, airaccount.aastar.eth, etc.
3. third level is free to register for different service providers, like jason.paymaster.aastar.eth
4. for specific service, we have different request and response structure in json.
5. we have collection request and single request to service portal and single service provider.
6. we have reputations in collection request response.
   

