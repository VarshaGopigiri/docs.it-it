---
title: '&lt;baseAddressPrefixFilters&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8cab2a9a-c51f-4283-bb60-2ad0c274fd46
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 0a1c2e5e887ceaadf3db6f51991d53c3db8fb6ba
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="ltbaseaddressprefixfiltersgt"></a>&lt;baseAddressPrefixFilters&gt;
Rappresenta una raccolta di elementi di configurazione che specificano filtri pass-through che forniscono un meccanismo per scegliere le associazioni di Internet Information Services (IIS) appropriate quando l'applicazione [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] è ospitata in IIS.  
  
> [!WARNING]
>  \<baseAddressPrefixFilters > non riconosce "localhost", in alternativa, usare il nome completo del computer.  
  
 \<System. ServiceModel >  
\<ServiceHostingEnvironment >  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
<serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="string"/>  
     </baseAddressPrefixFilters>  
</serviceHostingEnvironment>  
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
 Nessuno.  
  
### <a name="child-elements"></a>Elementi figlio  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-baseaddressprefixfilter.md)|Aggiunge un elemento di configurazione che specifica un filtro di prefisso per gli indirizzi di base usati dall'host del servizio.|  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[\<serviceHostingEnvironment >](../../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)|Definisce il tipo del quale l'ambiente host del servizio crea un'istanza per un determinato trasporto.|  
  
## <a name="remarks"></a>Note  
 Un filtro dei prefissi fornisce ai provider di hosting condiviso una modalità per specificare quali URI devono essere usati dal servizio. Consente agli host condivisi di ospitare più applicazioni con indirizzi di base diversi per lo stesso schema nello stesso sito.  
  
 I siti Web IIS sono contenitori di applicazioni virtuali che contengono directory virtuali. È possibile accedere all'applicazione in un sito tramite una o più associazioni IIS. Le associazioni IIS forniscono due tipi di informazioni: un protocollo di associazione e informazioni di associazione. Il protocollo di associazione, ad esempio HTTP, definisce lo schema in base al quale viene stabilita la comunicazione, mentre le informazioni di associazione, ad esempio l'indirizzo IP, la porta, l'intestazione host, contengono i dati usati per accedere al sito.  
  
 IIS supporta la definizione di più associazioni IIS per ogni sito, che si traduce in più indirizzi di base per ogni schema. Poiché un servizio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] ospitato in un sito consente l'associazione a un solo indirizzo di base per ogni schema, è possibile usare la funzionalità di filtro dei prefissi per scegliere l'indirizzo di base necessario per il servizio ospitato. Gli indirizzi di base in ingresso forniti da IIS sono filtrati in base all'elenco di prefissi facoltativo.  
  
 Un sito può ad esempio contenere gli indirizzi di base seguenti.  
  
```  
http://testl.fabrikam.com/Service.svc  
http://test2.fabrikam.com/Service.svc  
```  
  
 È possibile usare il file di configurazione seguente per specificare un filtro dei prefissi a livello di AppDomain.  
  
```xml  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="net.tcp://test1.fabrikam.com:8000"/>  
        <add prefix="http://test2.fabrikam.com:9000"/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 In questo esempio, `net.tcp://test1.fabrikam.com:8000` e `http://test2.fabrikam.com:9000` sono gli unici indirizzi di base che è consentito passare per i rispettivi schemi.  
  
 Per impostazione predefinita, quando non è specificato un prefisso, vengono passati tutti gli indirizzi. La definizione del prefisso fa in modo che venga passato solo l'indirizzo di base corrispondente allo schema specifico.  
  
> [!NOTE]
>  Il filtro non supporta caratteri jolly. Gli indirizzi di base forniti da IIS possono inoltre disporre di indirizzi associati ad altri schemi non presenti nell'elenco `baseAddressPrefixFilters`. Questi indirizzi non vengono filtrati.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Configuration.BaseAddressPrefixFilterElementCollection>  
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>  
 <xref:System.ServiceModel.ServiceHostingEnvironment>  
 [Hosting](../../../../../docs/framework/wcf/feature-details/hosting.md)
