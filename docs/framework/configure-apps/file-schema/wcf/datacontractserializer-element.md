---
title: '&lt;dataContractSerializer&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dataContractSerializer element
- <dataContractSerializer> element
- DataContractSerializer
- KnownTypes
ms.assetid: f41fb4d5-24e7-4059-8010-286a30bfea93
caps.latest.revision: "17"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 27b80c831fdc66bd3b022645c3de9c0c31ee575a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="ltdatacontractserializergt"></a>&lt;dataContractSerializer&gt;
Contiene dati di configurazione per <xref:System.Runtime.Serialization.DataContractSerializer>. Questo elemento è presente in due gerarchie diverse e viene elencato sia nella sezione Gerarchia dello schema seguente sia nella sezione Osservazioni.  
  
 \<System. ServiceModel >  
\<i comportamenti >  
\<serviceBehaviors >  
\<comportamento >  
\<dataContractSerializer >  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
<dataContractSerializer ignoreExtensionDataObject="Boolean"  
   maxItemsInObjectGraph="Integer" />  
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|IgnoreExtensionDataObject|Valore booleano che specifica se ignorare i dati forniti dall'endpoint quando vengono serializzati o deserializzati. Questo attributo è impostabile solo nell'elemento `<dataContractSerializer>` del serializzatore `<behavior>`.|  
|maxItemsInObjectGraph|Numero intero che specifica il numero massimo di elementi da serializzare o deserializzare. Questo attributo è pari a 65.536.|  
  
### <a name="child-elements"></a>Elementi figlio  
 Nessuno.  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[\<comportamento >](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md)|Raccolta di impostazioni per il comportamento di un servizio.|  
|[\<system.runtime.serialization>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-runtime-serialization.md)|Rappresenta l'elemento radice della sezione dello spazio dei nomi <xref:System.Runtime.Serialization> e contiene elementi per l'impostazione delle opzioni del serializzatore <xref:System.Runtime.Serialization.DataContractSerializer>.|  
  
## <a name="remarks"></a>Note  
 Come indicato nell'introduzione di questo argomento, questa è la seconda gerarchia in cui il \<X509Extension > si verifica l'elemento.  
  
 [\<system.runtime.serialization>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-runtime-serialization.md)  
  
 [\<dataContractSerializer >](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)  
  
 Per altre informazioni sui tipi noti, vedere <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>  
 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>  
 <xref:System.ServiceModel.Configuration.DataContractSerializerElement>  
 [Tipi noti di contratto di dati](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)  
 [Trasferimento e serializzazione dei dati](../../../../../docs/framework/wcf/feature-details/data-transfer-and-serialization.md)
