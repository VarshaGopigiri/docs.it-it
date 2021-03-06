---
title: Generatore EDM (EdmGen.exe)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe8297a1-1fc3-48ce-8eeb-f70f63f857aa
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 8d310786a12aa538a8a820c1c05788f30fe28c44
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="edm-generator-edmgenexe"></a>Generatore EDM (EdmGen.exe)
EdmGen.exe è uno strumento da riga di comando per l'uso di file di modello e di mapping [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]. Lo strumento EdmGen.exe consente di effettuare le operazioni seguenti:  
  
-   Connettersi a un'origine dati tramite un provider di dati .NET Framework specifico dell'origine dati e generare il modello concettuale, il modello di archiviazione e il file di mapping (rispettivamente con estensione csdl, ssdl e msl) usati da [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]. Per ulteriori informazioni, vedere [procedura: utilizzare EdmGen.exe per generare il modello e i file di Mapping](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).  
  
-   Convalidare un modello esistente. Per ulteriori informazioni, vedere [procedura: utilizzare EdmGen.exe per convalidare i file di modello e Mapping](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md).  
  
-   Generare un file di codice C# o Visual Basic contenente le classi di oggetti generate da un file del modello concettuale (con estensione csdl). Per ulteriori informazioni, vedere [procedura: utilizzare EdmGen.exe per generare codice del livello oggetti](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-object-layer-code.md).  
  
-   Generare un file di codice C# o Visual Basic contenente le visualizzazioni pregenerate per un modello esistente. Per ulteriori informazioni, [come: Pre-Generate viste per migliorare le prestazioni di Query](http://msdn.microsoft.com/library/b18a9d16-e10b-4043-ba91-b632f85a2579).  
  
 Lo strumento EdmGen.exe viene installato nella directory [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)]. In molti casi, il file si trova in C:\windows\Microsoft.NET\Framework\v4.0. Per i sistemi a 64 bit, questa directory si trova in C:\windows\Microsoft.NET\Framework64\v4.0. È inoltre possibile accedere lo strumento EdmGen.exe dal prompt dei comandi di Visual Studio (fare clic su **avviare**, scegliere **tutti i programmi**, scegliere **Microsoft Visual Studio 2010**, scegliere **Visual Studio Tools**, quindi fare clic su **Prompt dei comandi di Visual Studio 2010**).  
  
## <a name="syntax"></a>Sintassi  
  
```  
EdmGen /mode:choice [options]  
```  
  
## <a name="mode"></a>Modalità  
 Quando si usa lo strumento EdmGen.exe, è necessario specificare una delle modalità seguenti.  
  
|Modalità|Descrizione|  
|----------|-----------------|  
|`/mode:ValidateArtifacts`|Consente di convalidare i file con estensione csdl, ssdl e msl e di visualizzare eventuali errori o avvisi.<br /><br /> Questa opzione richiede almeno uno degli argomenti `/inssdl` o `/incsdl`. Se si specifica `/inmsl`, sono necessari anche gli argomenti `/inssdl` e `/incsdl`.|  
|`/mode:FullGeneration`|Consente di usare le informazioni sulla connessione al database specificate nell'opzione `/connectionstring` e di generare file con estensione csdl, ssdl e msl, nonché file di visualizzazione e del livello di oggetti.<br /><br /> Questa opzione richiede l'argomento `/connectionstring` e un argomento `/project` oppure gli argomenti `/outssdl`, `/outcsdl`, `/outmsdl`, `/outobjectlayer`, `/outviews`, `/namespace` e `/entitycontainer`.|  
|`/mode:FromSSDLGeneration`|Consente di generare file con estensione csdl e msl, codice sorgente e visualizzazioni dal file con estensione ssdl specificato.<br /><br /> Questa opzione richiede l'argomento `/inssdl` e un argomento `/project` oppure gli argomenti `/outcsdl`, `/outmsl`, `/outobjectlayer`, `/outviews`, `/namespace,` e `/entitycontainer`.|  
|`/mode:EntityClassGeneration`|Consente di creare un file di codice sorgente contenente le classi generate dal file con estensione csdl.<br /><br /> Questa opzione richiede l'argomento `/incsdl` e l'argomento `/project` o `/outobjectlayer`. L'argomento `/language` è facoltativo.|  
|`/mode:ViewGeneration`|Consente di creare un file di codice sorgente contenente le visualizzazioni generate dai file con estensione csdl, ssdl e msl.<br /><br /> Questa opzione richiede l'argomento `/inssdl`, `/incsdl`, `/inmsl,` e gli argomenti `/project` o `/outviews`. L'argomento `/language` è facoltativo.|  
  
## <a name="options"></a>Opzioni  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|`/p[roject]:`\<string>|Consente di specificare il nome del progetto da usare. Il nome del progetto viene usato come impostazione predefinita per la configurazione dello spazio dei nomi, il nome dei file di modello e di mapping, il nome del file di origine degli oggetti e il nome del file di origine di generazione delle visualizzazioni. Il nome del contenitore di entità è impostata su \<progetto > contesto.|  
|`/prov[ider]:`\<string>|Nome del provider di dati [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] da usare per generare il file del modello di archiviazione (con estensione ssdl). Il provider predefinito è il [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] Provider di dati per SQL Server (<xref:System.Data.SqlClient?displayProperty=nameWithType>).|  
|`/c[onnectionstring]:`\<stringa di connessione >|Consente di specificare la stringa usata per la connessione all'origine dati.|  
|`/incsdl:`\<file>|Consente di specificare il file con estensione csdl o una directory contenente i file con questa estensione. Questo argomento può essere specificato più volte in modo che sia possibile indicare più directory o file con estensione csdl. La specifica di più directory può essere utile per generare classi (`/mode:EntityClassGeneration`) o visualizzazioni (`/mode:ViewGeneration`) quando il modello concettuale è suddiviso in più file. Può inoltre risultare utile quando si desidera convalidare più modelli (`/mode:ValidateArtifacts`).|  
|`/refcsdl:`\<file>|Consente di specificare il file con estensione csdl aggiuntivo o i file usati per risolvere qualsiasi riferimento nel file con estensione csdl di origine. Il file con estensione csdl di origine è il file specificato dall'opzione `/incsdl`. Il file `/refcsdl` contiene i tipi da cui dipende il file con estensione csdl di origine. Questo argomento può essere specificato più volte.|  
|`/inmsl:`\<file>|Consente di specificare il file con estensione msl o una directory contenente i file con questa estensione. Questo argomento può essere specificato più volte in modo che sia possibile indicare più directory o file con estensione msl. La specifica di più directory può essere utile per generare visualizzazioni (`/mode:ViewGeneration`) quando il modello concettuale è suddiviso in più file. Può inoltre risultare utile quando si desidera convalidare più modelli (`/mode:ValidateArtifacts`).|  
|`/inssdl:`\<file>|Consente di specificare il file con estensione ssdl o una directory contenente i file con questa estensione. Questo argomento può essere specificato più volte in modo che sia possibile indicare più directory o file con estensione ssdl. Può risultare utile quando si desidera convalidare più modelli `(/mode:ValidateArtifacts)`.|  
|`/outcsdl:`\<file>|Consente di specificare il nome del file con estensione csdl che verrà creato.|  
|`/outmsl:`\<file>|Consente di specificare il nome del file con estensione msl che verrà creato.|  
|`/outssdl:`\<file>|Consente di specificare il nome del file con estensione ssdl che verrà creato.|  
|`/outobjectlayer:`\<file>|Consente di specificare il nome del file di codice sorgente contenente gli oggetti generati dal file con estensione csdl.|  
|`/outviews:`\<file>|Consente di specificare il nome del file di codice sorgente contenente le visualizzazioni generate.|  
|`/language:`[VB&#124;CSharp]|Consente di specificare il linguaggio per i file di codice sorgente generati. Il linguaggio predefinito è C#.|  
|`/namespace:`\<string>|Consente di specificare lo spazio dei nomi del modello da usare. Lo spazio dei nomi viene impostato nel file con estensione csdl quando si esegue `/mode:FullGeneration` o `/mode:FromSSDLGeneration`. Lo spazio dei nomi non viene usato quando si esegue `/mode:EntityClassGeneration`.|  
|`/entitycontainer:`\<string>|Consente di specificare il nome da applicare all'elemento `<EntityContainer>` nei file di modello e di mapping generati.|  
|`/pl[uralize]`|Applica le regole della lingua inglese per i singolari e i plurali ai nomi `Entity`, `EntitySet` e `NavigationProperty` nel modello concettuale. Questa opzione eseguirà le azioni seguenti:<br /><br /> -Verificare tutti `EntityType` nomi singolare.<br />-Verificare tutti `EntitySet` nomi plurali.<br />-Per ciascuna `NavigationProperty` che restituisce al massimo un'entità, renderà singolare il nome.<br />-Per ciascuna `NavigationProperty` che restituisce più di un'entità, specificare un nome plurale.|  
|`/SupressForeignKeyProperties or /nofk`|Impedisce l'esposizione di colonne di chiavi esterne come proprietà scalari sui tipi di entità nel modello concettuale.|  
|`/help` o `?`|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|`/nologo`|Consente di disattivare la visualizzazione del messaggio di copyright.|  
|`/targetversion:` \<string>|Versione di .NET Framework usata per compilare il codice generato. Le versioni supportate sono la 4 e la 4.5. Il valore predefinito è 4.|  
  
## <a name="in-this-section"></a>In questa sezione  
 [Procedura: Usare EdmGen.exe per generare i file di modello e di mapping](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)  
  
 [Procedura: Usare EdmGen.exe per generare codice a livello oggetti](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-object-layer-code.md)  
  
 [Procedura: Usare EdmGen.exe per convalidare file di modello e di mapping](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di ADO.NET Entity Data Model](http://msdn.microsoft.com/library/91076853-0881-421b-837a-f582f36be527)  
 [Entity Data Model](../../../../../docs/framework/data/adonet/entity-data-model.md)  
 [Specifiche CSDL, SSDL e MSL](../../../../../docs/framework/data/adonet/ef/language-reference/csdl-ssdl-and-msl-specifications.md)
