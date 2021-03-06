---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 05/16/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 55ac7e055c972a9b18ef374ac8498b418c5d56af
ms.sourcegitcommit: 688a394c4901590bbcf5351f9afdf9e8f0c89505
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/17/2018
ms.locfileid: "34307587"
---
|  | **Punkt-lokacja** | **Lokacja-lokacja** | **ExpressRoute** |
| --- | --- | --- | --- |
| **Usługi obsługiwane przez platformę Azure** |Usługi Cloud Services i Virtual Machines |Usługi Cloud Services i Virtual Machines |[Lista usług](../articles/expressroute/expressroute-faqs.md#supported-services) |
| **Typowe przepustowości** |Oparte na jednostce SKU bramy |Zwykle < 1 Gb/s łącznie |50 Mb/s, 100 Mb/s, 200 Mb/s, 500 Mb/s, 1 Gb/s, 2 Gb/s, 5 Gb/s, 10 Gb/s |
| **Obsługiwane protokoły** |Secure Sockets Tunneling Protocol (SSTP) i IPsec |IPsec |Bezpośrednie połączenie za pośrednictwem sieci VLAN, technologie VPN NSP (MPLS, VPLS itp.) |
| **Routing** |RouteBased (dynamiczny) |Firma Microsoft obsługuje routing typu PolicyBased (statyczny) i RouteBased (dynamiczny VPN) |BGP |
| **Elastyczność połączenia** |aktywne/pasywne |aktywne/pasywne lub aktywne/aktywne |aktywne/aktywne |
| **Typowy przypadek użycia** |Tworzenie prototypów, scenariusze laboratorium do tworzenia i testowania dla usług w chmurze i maszyn wirtualnych |Scenariusze laboratorium do tworzenia i testowania oraz obciążenia produkcyjne o małej skali dla usług w chmurze i maszyn wirtualnych |Dostęp do wszystkich usług Azure (zatwierdzona lista), obciążenia o znaczeniu krytycznym oraz klasy korporacyjnej, Backup, dane big data, platforma Azure jako lokacja DR |
| **Umowa SLA** |[Umowa SLA](https://azure.microsoft.com/support/legal/sla/) |[Umowa SLA](https://azure.microsoft.com/support/legal/sla/) |[Umowa SLA](https://azure.microsoft.com/support/legal/sla/) |
| **Cennik** |[Cennik](https://azure.microsoft.com/pricing/details/vpn-gateway/) |[Cennik](https://azure.microsoft.com/pricing/details/vpn-gateway/) |[Cennik](https://azure.microsoft.com/pricing/details/expressroute/) |
| **Dokumentacja techniczna** |[Dokumentacja usługi VPN Gateway](https://azure.microsoft.com/documentation/services/vpn-gateway/) |[Dokumentacja usługi VPN Gateway](https://azure.microsoft.com/documentation/services/vpn-gateway/) |[Dokumentacja usługi ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) |
| **Często zadawane pytania** |[VPN Gateway — często zadawane pytania](../articles/vpn-gateway/vpn-gateway-vpn-faq.md) |[VPN Gateway — często zadawane pytania](../articles/vpn-gateway/vpn-gateway-vpn-faq.md) |[Usługa ExpressRoute — często zadawane pytania](../articles/expressroute/expressroute-faqs.md) |
