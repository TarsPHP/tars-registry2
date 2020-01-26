##Master addressing module



##1. Module description

` ` ` `

The tar registry service of the tar s platform provides the function of service discovery.

This module provides PHP with the ability of master addressing (service discovery).

` ` ` `
##2. Document description:
```
├── composer.json
├── src
│   ├── client  //Client code requesting the master service
│   │   ├── Code.php
│   │   ├── CodeRegistry.php
│   │   ├── CommunicatorConfig.php
│   │   ├── CommunicatorFactory.php
│   │   ├── Communicator.php
│   │   ├── CommunicatorRegistry.php
│   │   ├── Consts.php
│   │   ├── RequestPacket.php
│   │   ├── RequestPacketRegistry.php
│   │   ├── ResponsePacket.php
│   │   ├── ResponsePacketRegistry.php
│   │   ├── TUPAPIWrapper.php
│   │   └── TUPAPIWrapperRegistry.php
│   ├── EndpointF.php       //struct EndpointF 的php类
│   ├── QueryFServant.php   //Direct request for master service
│   ├── QueryFWrapper.php   //The priority is to find the service address from memory, and then from the master address
│   ├── RouteTable.php      //Save the service address in the swoole table
│   └── tars   //Protocol file            
│       ├── EndpointF.tars 
│       └── QueryF.tars 
└── tests
    └── demo.php

```

## 3、Use example:
```
        //从tarsregistryService search service address
        $wrapper = new \Tars\registry\QueryFWrapper("tars.tarsregistry.QueryObj@tcp -h 172.16.0.161 -p 17890",1,60000);
        $result = $wrapper->findObjectById("PHPTest.PHPServer.obj");
        var_dump($result);

        //The priority is to find the service address from memory, and then from the master address
        \Tars\registry\RouteTable::getInstance();
        $result = \Tars\registry\RouteTable::getRouteInfo("PHPTest.PHPServer.obj");
        echo "result:\n";
        var_dump($result);
```

## 4. Changelog

### v0.1.7 (2019-03-20)
* Master addressing cache interface, convenient to customize cache mode, default to use swoole table
