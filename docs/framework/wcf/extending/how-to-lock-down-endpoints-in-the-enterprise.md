---
title: 'Procedura: bloccare gli endpoint nell''organizzazione'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1b7eaab7-da60-4cf7-9d6a-ec02709cf75d
caps.latest.revision: "21"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 5b6fa36a269dec4a191417813ec9c4ee26b699ee
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-lock-down-endpoints-in-the-enterprise"></a>Procedura: bloccare gli endpoint nell'organizzazione
Le aziende di grandi dimensioni spesso richiedono che le applicazioni vengano sviluppate in conformità con i criteri di sicurezza aziendali. Nell'argomento seguente viene illustrato come installare e sviluppare un validator dell'endpoint client che può essere usato per convalidare tutte le applicazioni client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] installate nei computer.  
  
 In questo caso, il validator è un validator client perché questo comportamento dell'endpoint viene aggiunto al client [ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) sezione nel file Machine. config. In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono caricati i comportamenti dell'endpoint comuni solo per le applicazioni client e i comportamenti del servizio comuni solo per le applicazioni di servizio. Per installare questo stesso validator per le applicazioni di servizio, il validator deve essere un comportamento del servizio. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]il [ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) sezione.  
  
> [!IMPORTANT]
>  Comportamenti del servizio o dell'endpoint non contrassegnati con il <xref:System.Security.AllowPartiallyTrustedCallersAttribute> attributo (APTCA) aggiunti al [ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) sezione di un file di configurazione non vengono eseguiti quando l'applicazione in esecuzione in una relazione di trust parziale ambiente e non l'eccezione viene generata in questo caso. Per imporre l'esecuzione di comportamenti comuni, ad esempio validator, è necessario:  
>   
>  -- Contrassegnare il proprio comportamento comune con l'attributo <xref:System.Security.AllowPartiallyTrustedCallersAttribute> in modo tale che questo possa essere eseguito se distribuito come applicazione parzialmente attendibile. Si noti che è possibile impostare nel computer una voce di registro per impedire l'esecuzione degli assembly APTCA.  
>   
>  -- Verificare che, se l'applicazione viene distribuita come completamente attendibile, gli utenti non possano modificare le impostazioni di sicurezza per l'accesso al codice per eseguire l'applicazione in ambiente parzialmente attendibile. In tal caso, il validator personalizzato non viene eseguito e non viene generata alcuna eccezione. Per un modo per verificare il, vedere il `levelfinal` tramite [strumento Criteri di sicurezza dall'accesso di codice (Caspol.exe)](http://go.microsoft.com/fwlink/?LinkId=248222).  
>   
>  Per ulteriori informazioni, vedere [parziale Trust consigliate](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md) e [scenari di distribuzione supportati](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md).  
  
### <a name="to-create-the-endpoint-validator"></a>Creazione del validator dell'endpoint.  
  
1.  Creare un oggetto <xref:System.ServiceModel.Description.IEndpointBehavior> con i passaggi di convalida desiderati nel metodo <xref:System.ServiceModel.Description.IEndpointBehavior.Validate%2A>. Nel codice seguente ne viene illustrato un esempio. (Il `InternetClientValidatorBehavior` da cui proviene il [convalida di sicurezza](../../../../docs/framework/wcf/samples/security-validation.md) esempio.)  
  
     [!code-csharp[LockdownValidation#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorbehavior.cs#2)]  
  
2.  Creare un nuovo oggetto <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> che registra il validator dell'endpoint creato nel passaggio 1. Nell'esempio di codice seguente viene illustrata questa operazione. (Il codice originale per questo esempio è la [convalida di sicurezza](../../../../docs/framework/wcf/samples/security-validation.md) esempio.)  
  
     [!code-csharp[LockdownValidation#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorelement.cs#3)]  
  
3.  Verificare che l'assembly compilato sia firmato con un nome sicuro. Per informazioni dettagliate, vedere il [strumento nome sicuro (SN. Con estensione EXE)](http://go.microsoft.com/fwlink/?LinkId=248217) e i comandi del compilatore per la propria lingua.  
  
### <a name="to-install-the-validator-into-the-target-computer"></a>Installazione del validator nel computer di destinazione  
  
1.  Installare il validator dell'endpoint usando il meccanismo appropriato. In un'azienda, è possibile usare a tale fine Criteri di gruppo e Systems Management Server (SMS).  
  
2.  Installare l'assembly con nome sicuro nella global assembly cache mediante il [Gacutil.exe (strumento Global Assembly Cache)](http://msdn.microsoft.com/library/ex0ss12c\(v=vs.110\).aspx).  
  
3.  Usare i tipi di spazio dei nomi <xref:System.Configuration?displayProperty=nameWithType> per:  
  
    1.  Aggiungere l'estensione per il [ \<behaviorExtensions >](../../../../docs/framework/configure-apps/file-schema/wcf/behaviorextensions.md) sezione usando un nome completo e bloccare l'elemento.  
  
         [!code-csharp[LockdownValidation#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#5)]  
  
    2.  Aggiungere l'elemento di comportamento per la `EndpointBehaviors` proprietà del [ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) sezione e bloccare l'elemento. Per installare un validator nel servizio, tale validator deve essere un <xref:System.ServiceModel.Description.IServiceBehavior> e deve essere aggiunto alla proprietà `ServiceBehaviors`. Nel seguente esempio di codice viene illustrata la configurazione corretta dopo i passaggi a. e b., con la sola eccezione che non è presente un nome sicuro.  
  
         [!code-csharp[LockdownValidation#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#6)]  
  
    3.  Salvare il file machine.config. Nell'esempio di codice seguente vengono eseguite tutte le attività nel passaggio 3, ma viene salvata localmente una copia del file machine.config modificato.  
  
         [!code-csharp[LockdownValidation#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#7)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene illustrato come aggiungere un comportamento comune al file machine.config e salvare una copia sul disco. Il `InternetClientValidatorBehavior` da cui proviene il [convalida di sicurezza](../../../../docs/framework/wcf/samples/security-validation.md) esempio.  
  
 [!code-csharp[LockdownValidation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#1)]  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Si potrebbe inoltre desiderare di crittografare gli elementi del file di configurazione. Per altre informazioni, vedere la sezione Vedere anche.  
  
## <a name="see-also"></a>Vedere anche  
 [Crittografia degli elementi di file di configurazione con DPAPI](http://go.microsoft.com/fwlink/?LinkId=94954)  
 [Crittografia degli elementi di file di configurazione con RSA](http://go.microsoft.com/fwlink/?LinkId=94955)
