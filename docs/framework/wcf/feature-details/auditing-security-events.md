---
title: Controllo degli eventi di sicurezza
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: auditing security events [WCF]
ms.assetid: 5633f61c-a3c9-40dd-8070-1c373b66a716
caps.latest.revision: "27"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: cb8f112c71c743fd6650baf04b8db55ceaeef4ae
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="auditing-security-events"></a>Controllo degli eventi di sicurezza
Le applicazioni create in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] possono utilizzare una funzionalità di controllo che consente di registrare gli eventi di sicurezza in base all'esito: è possibile registrare solo gli eventi con esito positivo, solo gli eventi con esito negativo o entrambi. Gli eventi vengono scritti nel registro eventi del sistema Windows e possono essere esaminati tramite il Visualizzatore eventi.  
  
 La funzionalità di controllo consente a un amministratore di individuare un attacco mentre è ancora in corso o quando è già avvenuto. Tale funzionalità consente inoltre agli sviluppatori di semplificare il debug dei problemi di sicurezza. Ad esempio, se per un errore nella configurazione dei criteri di autorizzazione o di verifica il sistema nega l'accesso a un utente autorizzato, uno sviluppatore può individuare e isolare rapidamente la causa di questo errore esaminando il registro eventi.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sicurezza, vedere [Cenni preliminari sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-overview.md). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]programmazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [programmazione WCF di base](../../../../docs/framework/wcf/basic-wcf-programming.md).  
  
## <a name="audit-level-and-behavior"></a>Livelli e comportamenti di controllo  
 Esistono due livelli di controllo di sicurezza:  
  
-   Livello Autorizzazione servizio, che prevede l'autorizzazione di un chiamante.  
  
-   Livello Messaggio, in cui [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verifica la validità del messaggio e autentica il chiamante.  
  
 È possibile controllare controllo su entrambi i livelli per esito positivo o negativo, che è noto come il *comportamento di controllo*.  
  
## <a name="audit-log-location"></a>Posizione del registro di controllo  
 Dopo aver determinato un livello e un comportamento di controllo, è possibile specificare la posizione del registro di controllo. Sono disponibili tre opzioni: Predefinito, Applicazione e Protezione. Quando si specifica l'opzione Predefinito, la posizione effettiva del registro varia in base al sistema utilizzato e alla possibilità di quest'ultimo di supportare la scrittura nel registro di sicurezza. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la sezione "Sistema operativo" più avanti in questo argomento.  
  
 Per scrivere nel registro protezione è necessario disporre del privilegio `SeAuditPrivilege`. Per impostazione predefinita, solo gli account Sistema locale e Servizio di rete dispongono di questo privilegio. Per gestire le funzioni del registro protezione `read` e `delete` è necessario disporre del privilegio `SeSecurityPrivilege`. Per impostazione predefinita, solo gli amministratori dispongono di questo privilegio.  
  
 Gli utenti autenticati possono invece leggere e scrivere nel registro applicazioni. Per impostazione predefinita, il sistema operativo [!INCLUDE[wxp](../../../../includes/wxp-md.md)] scrive eventi di controllo in tale registro. Il registro applicazioni può inoltre contenere informazioni personali a cui tutti gli utenti autenticati sono in grado di accedere.  
  
## <a name="suppressing-audit-failures"></a>Soppressione degli errori di controllo  
 Durante il controllo è inoltre disponibile un'opzione che consente di sopprimere tutti gli errori di controllo. Per impostazione predefinita, gli errori di controllo non influiscono sulle applicazioni. Tuttavia, se occorre, è possibile impostare tale opzione su `false`. In questo modo, se si verifica un errore di controllo, viene generata un'eccezione.  
  
## <a name="programming-auditing"></a>Programmazione del controllo  
 Il comportamento di controllo può essere specificato a livello di programmazione o tramite configurazione.  
  
### <a name="auditing-classes"></a>Classi di controllo  
 Nella seguente tabella sono descritte le classi e le proprietà utilizzate per programmare un comportamento di controllo.  
  
|Classe|Descrizione|  
|-----------|-----------------|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>|Consente di impostare le opzioni di controllo come comportamento di servizio.|  
|<xref:System.ServiceModel.AuditLogLocation>|Enumerazione che consente di specificare la posizione del registro in cui scrivere. I valori possibili sono Predefinito, Applicazione e Protezione. Quando si seleziona Predefinito, il sistema operativo determina la posizione effettiva del registro. Per ulteriori informazioni, vedere la sezione "Scelta fra registro eventi Applicazione o Protezione" del presente argomento.|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.MessageAuthenticationAuditLevel%2A>|Specifica il livello Messaggio utilizzato per i controlli a livello di messaggio. Sono disponibili le opzioni `None`, `Failure`, `Success`, e `SuccessOrFailure`.|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.ServiceAuthorizationAuditLevel%2A>|Specifica il livello Autorizzazione servizio utilizzato per i controlli a livello di servizio. Sono disponibili le opzioni `None`, `Failure`, `Success`, e `SuccessOrFailure`.|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A>|Specifica la modalità di elaborazione della richiesta del client quando un controllo ha esito negativo. Ciò ad esempio si verifica quando il servizio tenta di scrivere nel registro protezione senza tuttavia disporre del privilegio `SeAuditPrivilege`. Il valore predefinito `true` indica che gli errori vengono ignorati e che la richiesta del client viene elaborata normalmente.|  
  
 Per un esempio di configurazione di un'applicazione di registrare eventi di controllo, vedere [procedura: controllare gli eventi di sicurezza](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md).  
  
### <a name="configuration"></a>Configurazione  
 È inoltre possibile utilizzare configurazione per specificare il comportamento di controllo aggiungendo un [ \<serviceSecurityAudit >](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md) sotto il [ \<comportamenti >](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md). È necessario aggiungere l'elemento in un [ \<comportamento >](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) come illustrato nel codice seguente.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <behavior>  
        <!— auditLogLocation="Application" or "Security" -—>  
        <serviceSecurityAudit  
                  auditLogLocation="Application"  
                  suppressAuditFailure="true"  
                  serviceAuthorizationAuditLevel="Failure"  
                  messageAuthenticationAuditLevel="SuccessOrFailure" />   
      </behavior>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 Se il controllo è attivo e non è stata specificata alcuna posizione `auditLogLocation`, la posizione predefinita del registro è "Protezione" se la piattaforma supporta la scrittura in tale registro. In caso contrario, tale posizione è "Applicazione". Solo i sistemi operativi [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] e [!INCLUDE[wv](../../../../includes/wv-md.md)] supportano la scrittura nel registro di sicurezza. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la sezione "Sistema operativo" più avanti in questo argomento.  
  
## <a name="security-considerations"></a>Considerazioni sulla sicurezza  
 Un utente malintenzionato a conoscenza del fatto che il controllo è attivo può inviare messaggi non validi che comportano la scrittura di voci di controllo. Ciò comporta a sua volta la generazione di errori nel sistema di controllo. Per ridurre questo problema, impostare la proprietà <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> su `true` e usare le proprietà del Visualizzatore eventi per controllare il comportamento di controllo. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]l'articolo del supporto Microsoft nella visualizzazione e gestione dei registri eventi mediante il Visualizzatore eventi in Windows XP, disponibile all'indirizzo [come visualizzare e gestire i registri eventi nel Visualizzatore eventi in Windows XP](http://go.microsoft.com/fwlink/?LinkId=89150).  
  
 Gli eventi di controllo scritti nel registro applicazioni in [!INCLUDE[wxp](../../../../includes/wxp-md.md)] sono visualizzabili da qualsiasi utente autenticato.  
  
## <a name="choosing-between-application-and-security-event-logs"></a>Scelta fra registro eventi Applicazione o Protezione  
 Nelle tabelle seguenti sono fornite informazioni per scegliere se eseguire la registrazione nel registro eventi Applicazione o nel registro eventi Protezione.  
  
#### <a name="operating-system"></a>Sistema operativo  
  
|System|Registro applicazioni|Registro protezione|  
|------------|---------------------|------------------|  
|[!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] o versione successiva|Supportato|Non supportato|  
|[!INCLUDE[ws2003sp1](../../../../includes/ws2003sp1-md.md)] e [!INCLUDE[wv](../../../../includes/wv-md.md)]|Supportato|Il contesto del thread deve disporre del privilegio `SeAuditPrivilege`|  
  
#### <a name="other-factors"></a>Altri fattori  
 Oltre al sistema operativo, nella tabella seguente sono descritte le altre impostazioni che controllano l'attivazione della registrazione.  
  
|Fattore|Registro applicazioni|Registro protezione|  
|------------|---------------------|------------------|  
|Gestione dei criteri di controllo|Non applicabile.|Insieme alla configurazione, il registro protezione viene controllato anche in base ai criteri LSA (Local Security Authority, autorità di sicurezza locale). È inoltre necessario attivare la categoria "Controlla accesso agli oggetti".|  
|Esperienza utente predefinita|Tutti gli utenti autenticati possono scrivere nel registro applicazioni. Di conseguenza, per i processi delle applicazioni non è necessario eseguire alcun passaggio aggiuntivo di autorizzazione.|Il processo dell'applicazione (ovvero il relativo contesto) deve disporre del privilegio `SeAuditPrivilege`.|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>  
 <xref:System.ServiceModel.AuditLogLocation>  
 [Panoramica della sicurezza](../../../../docs/framework/wcf/feature-details/security-overview.md)  
 [Programmazione WCF di base](../../../../docs/framework/wcf/basic-wcf-programming.md)  
 [Procedura: Controllare gli eventi di sicurezza](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)  
 [\<serviceSecurityAudit >](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md)  
 [\<i comportamenti >](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)  
 [Modello di sicurezza per Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
