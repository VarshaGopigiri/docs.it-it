---
title: '&lt;webHttpEndpoint&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ecaaeb6f-ebd0-411d-8b53-92477cd45347
caps.latest.revision: "2"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: fc45511e0e7b4644704a834f0bc08d64ff3367f3
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="ltwebhttpendpointgt"></a>&lt;webHttpEndpoint&gt;
Questo elemento di configurazione definisce un endpoint standard con fisse [ \<webHttpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md) automaticamente l'associazione che aggiunge il [ \<webHttp >](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md) comportamento. Usare questo endpoint per la scrittura di un servizio REST.  
  
\<System. ServiceModel >  
\<standardEndpoints >  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>
    <webHttpEndpoint>
      <standardEndpoint automaticFormatSelectionEnabled="String" 
                        defaultOutgoingResponseFormat="Xml/Json" 
                        helpEnabled="Boolean" 
                        webEndpointType="String"/>
    </webHttpEndpoint>
  </standardEndpoints>  
</system.serviceModel>  
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|automaticFormatSelectionEnabled|Valore booleano che indica se la selezione automatica del formato è abilitata.<br /><br /> Quando la selezione automatica del formato è abilitata, l'infrastruttura analizza l'intestazione `Accept` del messaggio di richiesta e determina il formato appropriato per la risposta. Se l'intestazione `Accept` non specifica un formato adatto per la risposta, l'infrastruttura usa il `Content-Type` del messaggio di richiesta o il formato della risposta predefinito dell'operazione.|  
|defaultOutgoingResponseFormat|Attributo che specifica il formato predefinito per la risposta in uscita. L'attributo è di tipo <xref:System.ServiceModel.Web.WebMessageFormat>.|  
|helpEnabled|Valore booleano che indica se la Guida HTTP è abilitata per l'endpoint.|  
|webEndpointType|Stringa che specifica il tipo dell'endpoint.|  
  
### <a name="child-elements"></a>Elementi figlio  
 Nessuno.  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[\<standardEndpoints >](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Raccolta di endpoint standard rappresentati da endpoint predefiniti con una o più delle relative proprietà (indirizzo, associazione, contratto) fisse.|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Description.WebHttpEndpoint>  
 <xref:System.ServiceModel.Configuration.WebHttpEndpointElement>
