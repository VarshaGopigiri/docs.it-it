---
title: Attestazioni e token SAML
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
- WCF, federation
- federation
- issued tokens
- SAML token
ms.assetid: 930b6e34-9eab-4e95-826c-4e06659bb977
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: a2b35ba4da503663a2bb92597ed193c408e7c99b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="saml-tokens-and-claims"></a>Attestazioni e token SAML
Sicurezza asserzioni Markup Language (SAML) *token* sono rappresentazioni XML di attestazioni. Per impostazione predefinita, i token SAML [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene usato negli scenari di sicurezza federata *i token rilasciati*.  
  
 I token SAML contengono istruzioni che si configurano come attestazioni elaborate da un'entità su un'altra entità. Negli scenari di sicurezza federati, ad esempio, le istruzioni sono elaborate da un servizio token di sicurezza su un utente del sistema. Il servizio token di sicurezza firma il token SAML per indicare la veridicità delle istruzioni contenute nel token. Il token SAML, inoltre, è associato a chiavi crittografiche di cui l'utente del token SAML dimostra di essere a conoscenza. La prova dimostra al componente che il token SAML è stato, infatti, rilasciato a quell'utente. In uno scenario tipico, ad esempio:  
  
1.  Un client chiede un token SAML a un servizio token di sicurezza, autenticandosi al servizio mediante le credenziali di Windows.  
  
2.  Il servizio token di sicurezza rilascia un token SAML al cliente. Il token SAML viene firmato con un certificato associato al servizio token di sicurezza e contiene una chiave di prova crittografata per il servizio di destinazione.  
  
3.  Il client riceve inoltre una copia del *chiave di prova*. Il client presenta quindi il token SAML al servizio dell'applicazione (il *relying party*) e firma il messaggio con tale chiave di prova.  
  
4.  La firma sul token SAML dimostra al componente che il servizio token di sicurezza ha rilasciato il token. La firma del messaggio creata con la chiave di prova dimostra al componente che il token è stato rilasciato al client.  
  
## <a name="from-claims-to-samlattributes"></a>Da attestazioni a SamlAttributes  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] le istruzioni contenute nei token SAML sono modellate come oggetti <xref:System.IdentityModel.Tokens.SamlAttribute> che possono essere popolati direttamente da oggetti <xref:System.IdentityModel.Claims.Claim> purché l'oggetto <xref:System.IdentityModel.Claims.Claim> disponga di una proprietà <xref:System.IdentityModel.Claims.Claim.Right%2A> di <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> e la proprietà <xref:System.IdentityModel.Claims.Claim.Resource%2A> sia di tipo <xref:System.String>. Ad esempio:  
  
 [!code-csharp[c_CreateSTS#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#8)]
 [!code-vb[c_CreateSTS#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#8)]  
  
> [!NOTE]
>  Quando i token SAML vengono serializzati nei messaggi, quando sono rilasciati da un servizio token di sicurezza o quando sono presentati dai client ai servizi nell'ambito dell'autenticazione, la quota della dimensione massima del messaggio deve essere sufficientemente grande da contenere il token SAML e le altre parti del messaggio. Normalmente la quota della dimensione predefinita del messaggio è sufficiente. È tuttavia possibile, nei casi in cui un token SAML sia di grandi dimensioni perché contiene centinaia di attestazioni, che risulti necessario aumentare le quote per contenere il token serializzato. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Considerazioni sulla sicurezza per i dati](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md).  
  
## <a name="from-samlattributes-to-claims"></a>Da SamlAttributes ad attestazioni  
 Quando i token SAML vengono ricevuti nei messaggi, le varie istruzioni contenute nel token SAML vengono trasformate in oggetti <xref:System.IdentityModel.Policy.IAuthorizationPolicy> inseriti in <xref:System.IdentityModel.Policy.AuthorizationContext>. Le attestazioni di ogni istruzione SAML sono restituite dalla proprietà <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> di <xref:System.IdentityModel.Policy.AuthorizationContext> e possono essere esaminate per determinare se autenticare e autorizzare l'utente.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IdentityModel.Policy.AuthorizationContext>  
 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>  
 <xref:System.IdentityModel.Claims.ClaimSet>  
 [Federazione](../../../../docs/framework/wcf/feature-details/federation.md)  
 [Procedura: Creare un client federato](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)  
 [Procedura: Configurare le credenziali in un servizio federativo](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)  
 [Gestione delle attestazioni e dell'autorizzazione con il modello di identità](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)  
 [Attestazioni e token](../../../../docs/framework/wcf/feature-details/claims-and-tokens.md)  
 [Creazione di attestazioni e valori delle risorse](../../../../docs/framework/wcf/feature-details/claim-creation-and-resource-values.md)  
 [Procedura: Creare un'attestazione personalizzata](../../../../docs/framework/wcf/extending/how-to-create-a-custom-claim.md)
