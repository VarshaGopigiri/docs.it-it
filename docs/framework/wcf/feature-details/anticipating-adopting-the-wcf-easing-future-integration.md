---
title: 'Preparazione all''adozione di Windows Communication Foundation: facilitare l''integrazione futura'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3028bba8-6355-4ee0-9ecd-c56e614cb474
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 8dbb50af9d5655a76abb3827cd2f512eab0fd662
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="anticipating-adopting-the-windows-communication-foundation-easing-future-integration"></a>Preparazione all'adozione di Windows Communication Foundation: facilitare l'integrazione futura
Se si sta utilizzando ASP.NET ma si prevede di passare a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in futuro, in questo argomento vengono fornite indicazioni per assicurare il corretto funzionamento dei nuovi servizi Web ASP.NET con le applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## <a name="general-recommendations"></a>Suggerimenti generali  
 Adottare ASP.NET 2.0 per qualsiasi nuovo servizio. In tal modo sarà possibile accedere ai miglioramenti e ai potenziamenti della nuova versione. Sarà tuttavia possibile anche utilizzare i componenti ASP.NET 2.0 con i componenti [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nella stessa applicazione.  
  
## <a name="protocols"></a>Protocolli  
 Utilizzare la nuova funzionalità di ASP.NET 2.0 per convalidare la conformità a WS-I Basic Profile 1.1:  
  
```  
[WebService(Namespace = "http://tempuri.org/")]  
[WebServiceBinding(  
     ConformsTo = WsiProfiles.BasicProfile1_1,  
     EmitConformanceClaims=true)]  
public interface IEcho  
```  
  
 Per garantire l'interoperabilità tra i servizi Web ASP.NET conformi alla specifica WS-I Basic Profile 1.1 e i client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è possibile utilizzare un'associazione predefinita di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ovvero <xref:System.ServiceModel.BasicHttpBinding>.  
  
## <a name="service-development"></a>Sviluppo del servizio  
 Evitare di utilizzare l'attributo <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> per instradare i messaggi a metodi basati sul nome completo dell'elemento del corpo del messaggio SOAP anziché sull'intestazione HTTP SOAPAction. In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene utilizzata l'intestazione HTTP SOAPAction per instradare i messaggi.  
  
## <a name="data-representation"></a>Rappresentazione dei dati  
 Il codice XML in cui l'oggetto <xref:System.Xml.Serialization.XmlSerializer> serializza un tipo è per impostazione predefinita semanticamente identico al codice XML in cui l'oggetto <xref:System.Runtime.Serialization.DataContractSerializer> serializza un tipo, purché lo spazio dei nomi del codice XML sia stato definito in modo esplicito. Quando si definisce un tipo di dati da utilizzare in servizi Web ASP.NET perché si prevede di utilizzare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in futuro, eseguire le operazioni seguenti:  
  
1.  Definire il tipo utilizzando classi .NET Framework anziché l'XML Schema.  
  
2.  Aggiungere solo gli attributi <xref:System.SerializableAttribute> e <xref:System.Xml.Serialization.XmlRootAttribute> alla classe, utilizzando quest'ultimo per definire in modo esplicito lo spazio dei nomi del tipo. Evitare di aggiungere attributi aggiuntivi dallo spazio dei nomi <xref:System.Xml.Serialization> per controllare la modalità di conversione della classe .NET Framework in XML.  
  
 Tramite questo approccio è possibile convertire successivamente le classi .NET in contratti di dati aggiungendo gli attributi <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute> senza modificare in modo significativo il codice XML nel quale le classi vengono serializzate per la trasmissione. I tipi utilizzati nei messaggi dai servizi Web ASP.NET potranno essere elaborati come contratti di dati dalle applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Ciò offre diversi vantaggi, tra cui il miglioramento delle prestazioni delle applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## <a name="security"></a>Sicurezza  
 Evitare di utilizzare le opzioni di autenticazione fornite in Internet Information Services (IIS), poiché i client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non le supportano. Se occorre proteggere un servizio, utilizzare le opzioni fornite in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Queste opzioni sono infatti più affidabili e sono basate su protocolli standard.  
  
## <a name="see-also"></a>Vedere anche  
 [Preparazione all'adozione di Windows Communication Foundation: semplificazione della migrazione futura](../../../../docs/framework/wcf/feature-details/anticipating-adopting-wcf-migration.md)
