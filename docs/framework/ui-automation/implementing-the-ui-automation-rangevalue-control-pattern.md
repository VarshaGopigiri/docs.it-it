---
title: Implementazione del pattern di controllo RangeValue di automazione interfaccia utente
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- control patterns, Range Value
- Range Value control pattern
- UI Automation, Range Value control pattern
ms.assetid: 225feaa4-918e-418b-938e-7389338d0a69
caps.latest.revision: "19"
author: Xansky
ms.author: mhopkins
manager: markl
ms.workload: dotnet
ms.openlocfilehash: a53f5f802d451d7575188d4687b6d88f96ec64fb
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="implementing-the-ui-automation-rangevalue-control-pattern"></a>Implementazione del pattern di controllo RangeValue di automazione interfaccia utente
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere l'argomento sull' [API Automazione interfaccia utente di Windows](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono presentate le linee guida e le convenzioni per l'implementazione di <xref:System.Windows.Automation.Provider.IRangeValueProvider>, incluse le informazioni relative a eventi e proprietà. Alla fine della panoramica sono elencati collegamenti ad altro materiale di riferimento.  
  
 Il pattern di controllo <xref:System.Windows.Automation.RangeValuePattern> viene usato per supportare i controlli che possono impostare un valore in un intervallo. Per esempi di controlli che implementano questo pattern di controllo, vedere [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>Linee guida e convenzioni di implementazione  
 Quando si implementa il pattern di controllo RangeValue, tenere presenti le linee guida e le convenzioni seguenti:  
  
-   I controlli consentono la ricalibrazione delle relative proprietà supportate in base alle preferenze utente o alle impostazioni locali. Un esempio di questo è un controllo termometro che può essere impostato per visualizzare la temperatura in gradi Fahrenheit o Celsius.  
  
-   I controlli che dispongono di valori di intervallo ambigui, ad esempio le barre di avanzamento o i dispositivi di scorrimento, devono avere questi valori normalizzati.  
  
 ![Indicatore di stato. ] (../../../docs/framework/ui-automation/media/uia-rangevaluepattern-progress-bar.PNG "UIA_RangeValuePattern_Progress_Bar")  
Esempio di un indicatore di stato in cui valore è di tipo Integer e i relativi valori di proprietà minimo e massimo sono normalizzati rispettivamente a 0 e 100  
  
<a name="Required_Members_for_the_IRangeValueProvider"></a>   
## <a name="required-members-for-irangevalueprovider"></a>Membri obbligatori per IRangeValueProvider  
  
|Membro obbligatorio|Tipo di membro|Note|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.RangeValuePattern.IsReadOnlyProperty>|Proprietà|nessuno|  
|<xref:System.Windows.Automation.RangeValuePattern.ValueProperty>|Proprietà|nessuno|  
|<xref:System.Windows.Automation.RangeValuePattern.LargeChangeProperty>|Proprietà|nessuno|  
|<xref:System.Windows.Automation.RangeValuePattern.SmallChangeProperty>|Proprietà|nessuno|  
|<xref:System.Windows.Automation.RangeValuePattern.MaximumProperty>|Proprietà|nessuno|  
|<xref:System.Windows.Automation.RangeValuePattern.MinimumProperty>|Proprietà|nessuno|  
|<xref:System.Windows.Automation.RangeValuePattern.SetValue%2A>|Metodi|Nessuna|  
  
 Questo pattern di controllo non è associato a eventi.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>Eccezioni  
 I provider devono generare le eccezioni seguenti.  
  
|Tipo di eccezione|Condizione|  
|--------------------|---------------|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.RangeValuePattern.SetValue%2A> viene chiamato con un valore che è maggiore di <xref:System.Windows.Automation.RangeValuePattern.MaximumProperty> o minore di <xref:System.Windows.Automation.RangeValuePattern.MinimumProperty>.|  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica dei pattern di controllo per l'automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)  
 [Supportare pattern di controllo in un provider di automazione interfaccia utente](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)  
 [Pattern di controllo di automazione interfaccia utente per i client](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)  
 [Panoramica dell'albero di automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)  
 [Usare la memorizzazione nella cache in automazione interfaccia utente](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)
