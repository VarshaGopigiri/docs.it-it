---
title: 'Procedura: impostare una conferma della firma'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- signature confirmation
- WCF, security
ms.assetid: 2424c137-c7c2-4aa9-8d5d-a066e12fefda
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 53e38658671f3a36da67619c796667ecad61f286
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-set-up-a-signature-confirmation"></a>Procedura: impostare una conferma della firma
*Conferma della firma* è un meccanismo iniziatore del messaggio garantire che una risposta ricevuta sia stata generata in risposta al messaggio originale del mittente. La conferma della firma è definita nella specifica WS-Security 1.1. Se un endpoint supporta WS-Security 1.0, non è possibile utilizzare la conferma della firma.  
  
 Nelle procedure seguenti viene illustrato come consentire la conferma della firma utilizzando un <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>. È possibile utilizzare la stessa procedura con un <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>. La procedura si basa i passaggi di base, vedere [procedura: creare un personalizzato associazione usando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
### <a name="to-enable-signature-confirmation-in-code"></a>Per consentire la conferma della firma nel codice  
  
1.  Creare un'istanza della classe <xref:System.ServiceModel.Channels.BindingElementCollection>.  
  
2.  Creare un'istanza di <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> classe.  
  
3.  Impostare <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> su `true`.  
  
4.  Aggiungere l'elemento di sicurezza alla raccolta di associazioni.  
  
5.  Creare un'associazione personalizzata, come specificato in [procedura: creare un'associazione personalizzata usando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
### <a name="to-enable-signature-confirmation-in-configuration"></a>Per consentire la conferma della firma nella configurazione  
  
1.  Aggiungere un elemento `<customBinding>` alla sezione`<bindings>` del file di configurazione.  
  
2.  Aggiungere un elemento `<binding>` e impostare l'attributo del nome su un valore appropriato.  
  
3.  Aggiungere un elemento di codifica appropriato. Nell'esempio seguente viene aggiunto un elemento `<TextMessageEncoding>`.  
  
4.  Aggiungere un elemento figlio  `<security>`requireSignatureConfirmation e impostare l'attributo`requireSignatureConfirmation`true su`true`.  
  
5.  Facoltativo. Per abilitare la conferma della firma durante il programma di avvio, aggiungere un [ \<secureConversationBootstrap >](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) elemento figlio e i set di `equireSignatureConfirmation` attributo `true`.  
  
6.  Aggiungere un elemento di trasporto appropriato. L'esempio seguente aggiunge un [ \<httpTransport >](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md):  
  
    ```xml  
    <bindings>  
      <customBinding>  
        <binding name="SignatureConfirmationBinding">  
          <security requireSignatureConfirmation="true">  
            <secureConversationBootstrap requireSignatureConfirmation="true" />  
              </security>  
           <textMessageEncoding />  
             <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
## <a name="example"></a>Esempio  
 Nel codice seguente viene creata un'istanza di <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> e viene impostata la proprietà <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> su `true`. Si noti che in questo esempio non viene utilizzato l'elemento `<secureConversationBootstrap>` illustrato nell'esempio precedente. In questo esempio viene illustrata la conferma della firma quando si utilizza un token di Windows (protocollo Kerberos). In questo caso, la firma del client viene restituita in tutte le risposte dal servizio e viene confermata dal client.  
  
 [!code-csharp[c_SignatureConfirmation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_signatureconfirmation/cs/source.cs#1)]
 [!code-vb[c_SignatureConfirmation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_signatureconfirmation/vb/source.vb#1)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>  
 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>  
 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A>  
 [Procedura: Creare un'associazione personalizzata usando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 [Procedura: Creare un elemento SecurityBindingElement per una modalità di autenticazione specificata](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)
