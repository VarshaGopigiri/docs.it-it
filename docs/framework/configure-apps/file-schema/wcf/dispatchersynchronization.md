---
title: '&lt;dispatcherSynchronization&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cc030f9c-4e38-4b14-94dc-9a0e41ec8e2d
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 57477ea60337e5032b80bd9ae8da850099dd08f7
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="ltdispatchersynchronizationgt"></a>&lt;dispatcherSynchronization&gt;

Specifica un comportamento dell'endpoint che consente a un servizio di inviare risposte in modo asincrono.

\<System. ServiceModel > \<comportamenti > \<endpointBehaviors > \<comportamento >

## <a name="syntax"></a>Sintassi

```xml
<dispatcherSynchronizationBehavior asynchronousSendEnabled="Boolean" 
                                   maxPendingReceives="Integer" />
```

## <a name="type"></a>Tipo

`Type`

## <a name="attributes-and-elements"></a>Attributi ed elementi

Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.

### <a name="attributes"></a>Attributi

| Attributo               | Descrizione       |
| ----------------------- | ----------------- |
| asynchronousSendEnabled | Valore booleano che specifica se il comportamento di invio asincrono è abilitato. |
| `maxPendingReceives`    | Integer che specifica il numero di ricezioni simultanee che è possibile inviare sul canale.<br /><br /> Questo valore deve essere configurato solo dopo aver configurato correttamente il comportamento di limitazione del servizio. |

### <a name="child-elements"></a>Elementi figlio

Nessuno.

### <a name="parent-elements"></a>Elementi padre

| Elemento | Descrizione |  
| ------- | ----------- |  
| [\<comportamento >](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un comportamento dell'endpoint. |

## <a name="see-also"></a>Vedere anche

 <xref:System.ServiceModel.Configuration.DispatcherSynchronizationElement> <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior>
