---
title: Impostazioni del Registro di sistema ClearType
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ClearType [WPF], registry settings
- typography [WPF], ClearType registry settings
ms.assetid: 56f314bb-b30b-4f67-8492-8b8a9fa432ae
caps.latest.revision: "18"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: d915af4ee436bb6c661a7b412b0e36702191339a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="cleartype-registry-settings"></a>Impostazioni del Registro di sistema ClearType
In questo argomento viene fornita una panoramica di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_ct](../../../../includes/tlasharptla-ct-md.md)] le impostazioni del Registro di sistema utilizzate da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applicazioni.  
  
  
<a name="overview"></a>   
## <a name="technology-overview"></a>Informazioni generali sulla tecnologia  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]le applicazioni che eseguono il rendering di testo da un dispositivo di visualizzazione utilizzano [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] funzionalità per fornire una migliore esperienza di lettura. [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] è una tecnologia software sviluppata da [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] che consente di migliorare la leggibilità del testo sui display LCD (Liquid Crystal Display), ad esempio gli schermi di computer portatili, Pocket PC e i monitor a schermo piatto. Il funzionamento della tecnologia [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] si basa sull'accesso a singoli elementi striscia di colore verticali in ogni pixel di uno schermo LCD. Per ulteriori informazioni su [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)], vedere [ClearType Overview](../../../../docs/framework/wpf/advanced/cleartype-overview.md).  
  
 Testo che viene eseguito il rendering con [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] possono essere visualizzati in modo significativo diverso quando viene visualizzato su vari dispositivi di visualizzazione. Ad esempio, un numero ridotto di monitoraggi implementa strisce di colore in blu, verde, rosso ordine anziché più comune rosso, verde e blu ( [!INCLUDE[TLA#tla_rgb](../../../../includes/tlasharptla-rgb-md.md)]) ordine.  
  
 Testo che viene eseguito il rendering con [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] può inoltre avere significativamente diverso quando viene visualizzato da persone con livelli di sensibilità al colore. Alcune persone rilevano leggere differenze di colore meglio di altre.  
  
 In ognuno di questi casi, [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] funzionalità devono essere modificate per fornire la migliore esperienza di lettura per ogni singolo cliente.  
  
<a name="registry_settings"></a>   
## <a name="registry-settings"></a>Impostazioni Registro di sistema  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]Specifica i quattro impostazioni del Registro di sistema per il controllo [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] funzionalità:  
  
|Impostazione|Descrizione|  
|-------------|-----------------|  
|Livello [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)]|Descrive il livello di [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] colore maggiore chiarezza.|  
|Livello di gamma|Descrive il livello della componente cromatica del pixel per un dispositivo di visualizzazione.|  
|Struttura del pixel|Descrive la disposizione dei pixel per un dispositivo di visualizzazione.|  
|Livello di contrasto del testo|Descrive il livello di contrasto per il testo visualizzato.|  
  
 Queste impostazioni sono accessibili tramite un'utilità di configurazione esterni in grado di fare riferimento l'oggetto identificato [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] le impostazioni del Registro di sistema. Per creare o modificare queste impostazioni, è possibile accedere ai valori direttamente usando l'editor del Registro di sistema di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)].  
  
 Se il [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] le impostazioni del Registro di sistema non vengono impostate (stato predefinito), il [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] le query dell'applicazione di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] informazioni sui parametri di sistema per le impostazioni di smussatura dei caratteri.  
  
> [!NOTE]
>  Per informazioni sull'enumerazione dei nomi dei dispositivi di visualizzazione, vedere il `SystemParametersInfo` [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] (funzione).  
  
<a name="ClearType_level"></a>   
## <a name="cleartype-level"></a>Livello ClearType  
 Il [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] livello consente di regolare il rendering del testo in base alla sensibilità al colore e percezione di un singolo. Per alcune persone, il rendering del testo che utilizza [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] al livello più alto non genera la migliore esperienza di lettura.  
  
 Il [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] livello è un valore intero compreso tra 0 e 100. Il livello predefinito è 100, ovvero [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] utilizza la capacità massima di strisce di colore del dispositivo di visualizzazione. Tuttavia, un [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] livello pari a 0 esegue il rendering di testo in scala di grigi. Impostando il [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] livello tra 0 e 100, è possibile creare un livello intermedio adatto alla sensibilità al colore dei singoli.  
  
### <a name="registry-setting"></a>Impostazione del Registro di sistema  
 Il percorso di impostazione del Registro di sistema per il [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] livello è un'impostazione di singolo utente che corrisponde a un nome di dispositivo di visualizzazione specifico:  
  
 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 Per ogni nome di dispositivo di visualizzazione per un utente, un `ClearTypeLevel` è definito valore DWORD. Nella schermata seguente viene illustrata l'impostazione dell'Editor del Registro di sistema per il [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] livello.  
  
 ![Impostazioni ClearType nell'Editor del Registro di sistema](../../../../docs/framework/wpf/advanced/media/cleartyperegistry01.png "ClearTypeRegistry01")  
  
> [!NOTE]
>  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]le applicazioni il rendering del testo in uno dei scegliendo tra due modalità, con e senza [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)]. Quando viene eseguito il rendering testo senza [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)], viene indicato come per il rendering in scala di grigi.  
  
<a name="gamma_level"></a>   
## <a name="gamma-level"></a>Livello di gamma  
 Il livello di gamma fa riferimento alla relazione non lineare tra un valore in pixel e la luminanza. L'impostazione del livello di gamma deve corrispondere alle caratteristiche fisiche del dispositivo di visualizzazione, in caso contrario possono verificarsi distorsioni nell'output del rendering. Ad esempio, il testo potrebbe risultare troppo largo o troppo stretto o è possibile che compaiano sbavature di colore sui bordi dei gambi verticali dei glifi.  
  
 Il livello di gamma è un valore intero compreso tra 1000 e 2200. Il livello predefinito è 1900.  
  
### <a name="registry-setting"></a>Impostazione del Registro di sistema  
 Il percorso dell'impostazione del Registro di sistema per il livello di gamma è un'impostazione del computer locale che corrisponde al nome di uno specifico dispositivo di visualizzazione:  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 Per ogni nome di dispositivo di visualizzazione per un utente, un `GammaLevel` è definito valore DWORD. Lo screenshot seguente mostra l'impostazione dell'Editor del Registro di sistema per il livello di gamma.  
  
 ![Impostazioni ClearType nell'Editor del Registro di sistema](../../../../docs/framework/wpf/advanced/media/cleartyperegistry02.png "ClearTypeRegistry02")  
  
<a name="pixel_structure"></a>   
## <a name="pixel-structure"></a>Struttura del pixel  
 La struttura del pixel descrive il tipo di pixel alla base di un dispositivo di visualizzazione. La struttura del pixel è definita come uno di tre tipi:  
  
|Tipo|Valore|Descrizione|  
|----------|-----------|-----------------|  
|Semplice|0|Il dispositivo di visualizzazione non ha struttura del pixel. In questo caso le sorgenti di luce per ogni colore sono distribuite in modo uniforme nell'area dei pixel, condizione nota come rendering in scala di grigi. Questo è il funzionamento di un dispositivo di visualizzazione standard. [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] non viene mai applicato al testo di cui si esegue il rendering.|  
|RGB|1|Il dispositivo di visualizzazione dispone di pixel costituiti da tre strisce nell'ordine seguente: rosso, verde e blu. [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] viene applicato al testo di cui si esegue il rendering.|  
|BGR|2|Il dispositivo di visualizzazione dispone di pixel costituiti da tre strisce nell'ordine seguente: blu, verde e rosso. [!INCLUDE[TLA2#tla_ct](../../../../includes/tla2sharptla-ct-md.md)] viene applicato al testo di cui si esegue il rendering. Si noti come l'ordine viene invertito rispetto al tipo RGB.|  
  
 La struttura dei pixel corrisponde a un valore intero compreso tra 0 e 2. Il livello predefinito è 0, che rappresenta una struttura del pixel flat.  
  
> [!NOTE]
>  Per informazioni sull'enumerazione dei nomi dei dispositivi di visualizzazione, vedere il `EnumDisplayDevices` [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] (funzione).  
  
### <a name="registry-setting"></a>Impostazione del Registro di sistema  
 Il percorso dell'impostazione del Registro di sistema per la struttura del pixel è un'impostazione del computer locale che corrisponde al nome di uno specifico dispositivo di visualizzazione:  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 Per ogni nome di dispositivo di visualizzazione per un utente, un `PixelStructure` è definito valore DWORD. Lo screenshot seguente mostra l'impostazione dell'Editor del Registro di sistema per la struttura del pixel.  
  
 ![Impostazioni ClearType nell'Editor del Registro di sistema](../../../../docs/framework/wpf/advanced/media/cleartyperegistry02.png "ClearTypeRegistry02")  
  
<a name="text_contrast_level"></a>   
## <a name="text-contrast-level"></a>Livello di contrasto del testo  
 Il livello di contrasto del testo consente di regolare il rendering del testo in base alle larghezze del gambo dei glifi. Il livello di contrasto del testo è un valore intero compreso tra 0 e 6, dove il valore più grande indica una maggiore larghezza. Il livello predefinito è 1.  
  
### <a name="registry-setting"></a>Impostazione del Registro di sistema  
 Il percorso dell'impostazione del Registro di sistema per il livello di contrasto del testo è un'impostazione del singolo utente che corrisponde al nome di uno specifico dispositivo di visualizzazione:  
  
 `HKEY_CURRENT_USER\Software\Microsoft\Avalon.Graphics\<displayName>`  
  
 Per ogni nome di dispositivo di visualizzazione per un utente, un `TextContrastLevel` è definito valore DWORD. Lo screenshot seguente mostra l'impostazione dell'Editor del Registro di sistema per il livello di contrasto del testo.  
  
 ![Impostazioni ClearType nell'Editor del Registro di sistema](../../../../docs/framework/wpf/advanced/media/cleartyperegistry01.png "ClearTypeRegistry01")  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica su ClearType](../../../../docs/framework/wpf/advanced/cleartype-overview.md)  
 [ClearType Antialiasing (Anti-aliasing ClearType)](https://msdn.microsoft.com/library/dd183433(v=vs.85).aspx)
