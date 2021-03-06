---
title: Stringhe di formato TimeSpan personalizzate
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- format spexifiers, custom time interval
- format strings
- formatting [.NET Framework], time interval
- custom time interval format strings
- formatting [.NET Framework], time
- custom TimeSpan format strings
ms.assetid: a63ebf55-7269-416b-b4f5-286f6c03bf0e
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 7302b17beb5ce20ec2bd8865149fe2e0bae9cee4
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="custom-timespan-format-strings"></a>Stringhe di formato TimeSpan personalizzate
Oggetto <xref:System.TimeSpan> stringa di formato definisce la rappresentazione di stringa di un <xref:System.TimeSpan> valore risultante da un'operazione di formattazione. Una stringa di formato personalizzata è costituita da uno o più <xref:System.TimeSpan> identificatori insieme a qualsiasi numero di caratteri di formato. Qualsiasi stringa che non è un [stringa di formato TimeSpan standard](../../../docs/standard/base-types/standard-timespan-format-strings.md) viene interpretato come un oggetto personalizzato <xref:System.TimeSpan> stringa di formato.  
  
> [!IMPORTANT]
>  L'oggetto personalizzato <xref:System.TimeSpan> identificatori di formato non includono i simboli di separatori segnaposto, ad esempio i simboli per separare i giorni dalle ore, ore, minuti o secondi dai secondi frazionari. Questi simboli devono essere inclusi nella stringa di formato personalizzato come valori letterali stringa. Ad esempio, in `"dd\.hh\:mm"` il punto (.) è definito come separatore tra giorni e ore e i due punti (:) come separatore tra ore e minuti.  
>   
>  Inoltre, negli identificatori di formato <xref:System.TimeSpan> personalizzati non è incluso un simbolo di segno che consente di distinguere tra intervalli di tempo negativi e positivi. Per includere un simbolo di segno, è necessario creare una stringa di formato tramite la logica condizionale. Nella sezione [Altri caratteri](#Other) è incluso un esempio.  
  
 Rappresentazioni di stringa di <xref:System.TimeSpan> i valori vengono prodotte da chiamate agli overload del <xref:System.TimeSpan.ToString%2A?displayProperty=nameWithType> (metodo) e dai metodi che supportano la formattazione composita, ad esempio <xref:System.String.Format%2A?displayProperty=nameWithType>. Per altre informazioni, vedere [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md) e [Formattazione composita](../../../docs/standard/base-types/composite-formatting.md). Nell'esempio seguente viene illustrato l'utilizzo di stringhe di formato personalizzate nelle operazioni di formattazione.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customformatexample1.cs#1)]
 [!code-vb[Conceptual.TimeSpan.Custom#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customformatexample1.vb#1)]  
  
 Custom <xref:System.TimeSpan> stringhe di formato sono utilizzate anche dal <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> e <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> metodi per definire il formato richiesto di immettere le stringhe per le operazioni di analisi. (l'analisi converte la rappresentazione di stringa di un valore in tale valore). Nell'esempio seguente viene illustrato l'utilizzo di stringhe di formato standard nelle operazioni di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customparseexample1.cs#2)]
 [!code-vb[Conceptual.TimeSpan.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customparseexample1.vb#2)]  
  
<a name="table"></a>La tabella seguente descrive le date personalizzato e gli identificatori di formato di ora.  
  
|Identificatore di formato|Descrizione|Esempio|  
|----------------------|-----------------|-------------|  
|"d", "%d"|Il numero di giorni completi nell'intervallo di tempo.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "d"](#dSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%d` --> "6"<br /><br /> `d\.hh\:mm` --> "6.14:32"|  
|"dd"-"dddddddd"|Il numero di giorni completi nell'intervallo di tempo, con il numero di zeri necessari all'inizio.<br /><br /> Altre informazioni: ["dd"-"dddddddd" identificatori di formato personalizzati](#ddSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `ddd` --> "006"<br /><br /> `dd\.hh\:mm` --> "06.14:32"|  
|"h", "%h"|Il numero di ore complete nell'intervallo di tempo non conteggiate come parti di giorni. Le ore a una sola cifra non hanno uno zero iniziale.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "h"](#hSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%h` --> "14"<br /><br /> `hh\:mm` --> "14:32"|  
|"hh"|Il numero di ore complete nell'intervallo di tempo non conteggiate come parti di giorni. Le ore a una sola cifra hanno uno zero iniziale.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "hh"](#hhSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `hh` --> "14"<br /><br /> `new TimeSpan(6, 8, 32, 17, 685):`<br /><br /> `hh` --> 08|  
|"m", "%m"|Il numero di minuti completi nell'intervallo di tempo non conteggiati come parti di ore o di giorni. I minuti a una sola cifra non hanno uno zero iniziale.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "m"](#mSpecifier).|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `%m` --> "8"<br /><br /> `h\:m` --> "14:8"|  
|"mm"|Il numero di minuti completi nell'intervallo di tempo non conteggiati come parti di ore o di giorni. I minuti a una sola cifra hanno uno zero iniziale.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "mm"](#mmSpecifier).|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `mm` --> "08"<br /><br /> `new TimeSpan(6, 8, 5, 17, 685):`<br /><br /> `d\.hh\:mm\:ss` --> 6.08:05:17|  
|"s", "%s"|Il numero di secondi completi nell'intervallo di tempo non conteggiati come parti di minuti, ore o giorni. I secondi a una sola cifra non hanno uno zero iniziale.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "s"](#sSpecifier).|`TimeSpan.FromSeconds(12.965)`:<br /><br /> `%s` --> 12<br /><br /> `s\.fff` --> 12.965|  
|"ss"|Il numero di secondi completi nell'intervallo di tempo non conteggiati come parti di minuti, ore o giorni.  I secondi a una sola cifra hanno uno zero iniziale.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "ss"](#ssSpecifier).|`TimeSpan.FromSeconds(6.965)`:<br /><br /> `ss` --> 06<br /><br /> `ss\.fff` --> 06.965|  
|"f", "%f"|I decimi di secondo in un intervallo di tempo.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "f"](#fSpecifier).|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `f` --> 8<br /><br /> `ss\.f` --> 06.8|  
|"ff"|I centesimi di secondo in un intervallo di tempo.<br /><br /> Altre informazioni:[identificatore di formato personalizzato "ff"](#ffSpecifier).|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `ff` --> 89<br /><br /> `ss\.ff` --> 06.89|  
|"fff"|I millisecondi in un intervallo di tempo.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "fff"](#f3Specifier).|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `fff` --> 895<br /><br /> `ss\.fff` --> 06.895|  
|"ffff"|I decimillesimi di secondo in un intervallo di tempo.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "ffff"](#f4Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `ffff` --> 8954<br /><br /> `ss\.ffff` --> 06.8954|  
|"fffff"|I centesimi di millesimo di secondo in un intervallo di tempo.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "fffff"](#f5Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `fffff` --> 89543<br /><br /> `ss\.fffff` --> 06.89543|  
|"ffffff"|I milionesimi di secondo in un intervallo di tempo.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "ffffff"](#f6Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `ffffff` --> 895432<br /><br /> `ss\.ffffff` --> 06.895432|  
|"fffffff"|I decimilionesimi di secondo (o il numero frazionario di tick) in un intervallo di tempo.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "fffffff"](#f7Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `fffffff` --> 8954321<br /><br /> `ss\.fffffff` --> 06.8954321|  
|"F", "%F"|I decimi di secondo in un intervallo di tempo. Se la cifra è zero, non viene prodotta alcuna visualizzazione.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "F"](#F_Specifier).|`TimeSpan.Parse("00:00:06.32")`:<br /><br /> `%F`: 3<br /><br /> `TimeSpan.Parse("0:0:3.091")`:<br /><br /> `ss\.F`: 03.|  
|"FF"|I centesimi di secondo in un intervallo di tempo. Eventuali zeri finali frazionari o doppi zeri non sono inclusi.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FF"](#FF_Specifier).|`TimeSpan.Parse("00:00:06.329")`:<br /><br /> `FF`: 32<br /><br /> `TimeSpan.Parse("0:0:3.101")`:<br /><br /> `ss\.FF`: 03.1|  
|"FFF"|I millisecondi in un intervallo di tempo. Eventuali zeri finali frazionari non sono inclusi.<br /><br /> Ulteriori informazioni:|`TimeSpan.Parse("00:00:06.3291")`:<br /><br /> `FFF`: 329<br /><br /> `TimeSpan.Parse("0:0:3.1009")`:<br /><br /> `ss\.FFF`: 03.1|  
|"FFFF"|I decimillesimi di secondo in un intervallo di tempo. Eventuali zeri finali frazionari non sono inclusi.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FFFF"](#F4_Specifier).|`TimeSpan.Parse("00:00:06.32917")`:<br /><br /> `FFFFF`: 3291<br /><br /> `TimeSpan.Parse("0:0:3.10009")`:<br /><br /> `ss\.FFFF`: 03.1|  
|"FFFFF"|I centesimi di millesimo di secondo in un intervallo di tempo. Eventuali zeri finali frazionari non sono inclusi.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FFFFF"](#F5_Specifier).|`TimeSpan.Parse("00:00:06.329179")`:<br /><br /> `FFFFF`: 32917<br /><br /> `TimeSpan.Parse("0:0:3.100009")`:<br /><br /> `ss\.FFFFF`: 03.1|  
|"FFFFFF"|I milionesimi di secondo in un intervallo di tempo. Eventuali zeri finali frazionari non sono visualizzati.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FFFFFF"](#F6_Specifier).|`TimeSpan.Parse("00:00:06.3291791")`:<br /><br /> `FFFFFF`: 329179<br /><br /> `TimeSpan.Parse("0:0:3.1000009")`:<br /><br /> `ss\.FFFFFF`: 03.1|  
|"FFFFFFF"|I decimilionesimi di secondo in un intervallo di tempo. Eventuali zeri finali frazionari o gruppi di sette zeri non sono visualizzati.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FFFFFFF"](#F7_Specifier).|`TimeSpan.Parse("00:00:06.3291791")`:<br /><br /> `FFFFFF`: 3291791<br /><br /> `TimeSpan.Parse("0:0:3.1900000")`:<br /><br /> `ss\.FFFFFF`: 03.19|  
|*' stringa*'|Delimitatore di stringa letterale.<br /><br /> Altre informazioni: [altri caratteri](#Other).|`new TimeSpan(14, 32, 17):`<br /><br /> `hh':'mm':'ss` --> "14:32:17"|  
|\|Carattere di escape.<br /><br /> Altre informazioni:[altri caratteri](#Other).|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` --> "14:32:17"|  
|Qualsiasi altro carattere|Qualsiasi altro carattere senza escape viene interpretato come identificatore di formato personalizzato.<br /><br /> Ulteriori informazioni: [altri caratteri](#Other).|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` --> "14:32:17"|  
  
<a name="dSpecifier"></a>   
## <a name="the-d-custom-format-specifier"></a>Identificatore di formato personalizzato "d"  
 L'identificatore di formato personalizzato "d" restituisce il valore della <xref:System.TimeSpan.Days%2A?displayProperty=nameWithType> proprietà, che rappresenta il numero di giorni interi nell'intervallo di tempo. Restituisce il numero completo di giorni in un <xref:System.TimeSpan> valore, anche se il valore ha più di una cifra. Se il valore di <xref:System.TimeSpan.Days%2A?displayProperty=nameWithType> proprietà è zero, l'identificatore di output "0".  
  
 Se l'identificatore di formato personalizzato "d" viene usato da solo, specificare "%d" in modo che non venga interpretato erroneamente come stringa in formato standard. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#3)]
 [!code-vb[Conceptual.TimeSpan.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#3)]  
  
 Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "d".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#4)]
 [!code-vb[Conceptual.TimeSpan.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#4)]  
  
 [Torna alla tabella](#table)  
  
<a name="ddSpecifier"></a>   
## <a name="the-dd-dddddddd-custom-format-specifiers"></a>Identificatori di formato personalizzato "dd"-"dddddddd"  
 Il valore di output "dd", "ddd", "dddd", "ddddd", "dddddd", "ddddddd" e gli identificatori di formato personalizzato "dddddddd" il <xref:System.TimeSpan.Days%2A?displayProperty=nameWithType> proprietà, che rappresenta il numero di giorni interi nell'intervallo di tempo.  
  
 La stringa di output include un numero minimo di cifre specificato dal numero di caratteri "d" nell'identificatore di formato e il numero necessario di zeri iniziali. Se le cifre del numero di giorni superano il numero di caratteri "d"nell'identificatore di formato, l'output nella stringa risultato corrisponde al numero completo di giorni.  
  
 L'esempio seguente usa questi identificatori di formato per visualizzare la rappresentazione di stringa di due <xref:System.TimeSpan> valori. Il valore del componente giorni del primo intervallo di tempo è zero, mentre il valore del componente dei giorni del secondo è 365.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#5)]
 [!code-vb[Conceptual.TimeSpan.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="hSpecifier"></a>   
## <a name="the-h-custom-format-specifier"></a>Identificatore di formato personalizzato "h"  
 L'identificatore di formato personalizzato "h" restituisce il valore della <xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType> proprietà, che rappresenta il numero di ore intere nell'intervallo di tempo non conteggiati come parte del relativo componente giorno. Restituisce un valore di stringa di una cifra se il valore della <xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType> proprietà è da 0 a 9, e restituisce un valore di stringa di due cifre se il valore della <xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType> proprietà varia da 10 a 23.  
  
 Se l'identificatore di formato personalizzato "h" viene usato da solo, specificare "%h" in modo che non venga interpretato erroneamente come stringa in formato standard. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
 [!code-vb[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]  
  
 Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "%h" per interpretare la stringa numerica come numero di ore. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#8)]
 [!code-vb[Conceptual.TimeSpan.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#8)]  
  
 Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "h".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#7)]
 [!code-vb[Conceptual.TimeSpan.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#7)]  
  
 [Torna alla tabella](#table)  
  
<a name="hhSpecifier"></a>   
## <a name="the-hh-custom-format-specifier"></a>Identificatore di formato personalizzato "hh"  
 L'identificatore di formato personalizzato "hh" restituisce il valore della <xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType> proprietà, che rappresenta il numero di ore intere nell'intervallo di tempo non conteggiati come parte del relativo componente giorno. Per valori compresi tra 0 e 9, la stringa di output include uno zero iniziale.  
  
 Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "hh" per interpretare la stringa numerica come numero di ore. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#9)]
 [!code-vb[Conceptual.TimeSpan.Custom#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#9)]  
  
 Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "hh".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#10)]
 [!code-vb[Conceptual.TimeSpan.Custom#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#10)]  
  
 [Torna alla tabella](#table)  
  
<a name="mSpecifier"></a>   
## <a name="the-m-custom-format-specifier"></a>Identificatore di formato personalizzato "m"  
 L'identificatore di formato personalizzato "m" restituisce il valore della <xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType> proprietà, che rappresenta il numero di minuti interi nell'intervallo di tempo non conteggiati come parte del relativo componente giorno. Restituisce un valore di stringa di una cifra se il valore della <xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType> proprietà è da 0 a 9, e restituisce un valore di stringa di due cifre se il valore della <xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType> proprietà varia da 10 a 59.  
  
 Se l'identificatore di formato personalizzato "m" viene usato da solo, specificare "%m" in modo che non venga interpretato erroneamente come stringa in formato standard. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
 [!code-vb[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]  
  
 Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "%m" per interpretare la stringa numerica come numero di minuti. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#11)]
 [!code-vb[Conceptual.TimeSpan.Custom#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#11)]  
  
 Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "m".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#12)]
 [!code-vb[Conceptual.TimeSpan.Custom#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#12)]  
  
 [Torna alla tabella](#table)  
  
<a name="mmSpecifier"></a>   
## <a name="the-mm-custom-format-specifier"></a>Identificatore di formato personalizzato "mm"  
 L'identificatore di formato personalizzato "mm" restituisce il valore della <xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType> proprietà, che rappresenta il numero di minuti interi nell'intervallo di tempo che non è incluso come parte del componente ore o giorni. Per valori compresi tra 0 e 9, la stringa di output include uno zero iniziale.  
  
 Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "mm" per interpretare la stringa numerica come numero di minuti. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#13)]
 [!code-vb[Conceptual.TimeSpan.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#13)]  
  
 Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "mm".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#14)]
 [!code-vb[Conceptual.TimeSpan.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#14)]  
  
 [Torna alla tabella](#table)  
  
<a name="sSpecifier"></a>   
## <a name="the-s-custom-format-specifier"></a>Identificatore di formato personalizzato "s"  
 L'identificatore di formato personalizzato "s" restituisce il valore della <xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType> proprietà, che rappresenta il numero di secondi interi nell'intervallo di tempo che non è incluso come parte del relativo ore, giorni o componente di minuti. Restituisce un valore di stringa di una cifra se il valore della <xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType> proprietà è da 0 a 9, e restituisce un valore di stringa di due cifre se il valore della <xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType> proprietà varia da 10 a 59.  
  
 Se l'identificatore di formato personalizzato "s" viene usato da solo, specificare "%s" in modo che non venga interpretato erroneamente come stringa in formato standard. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#15)]
 [!code-vb[Conceptual.TimeSpan.Custom#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#15)]  
  
 Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "%s" per interpretare la stringa numerica come numero di secondi. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#17)]
 [!code-vb[Conceptual.TimeSpan.Custom#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#17)]  
  
 Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "s".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#16)]
 [!code-vb[Conceptual.TimeSpan.Custom#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#16)]  
  
 [Torna alla tabella](#table)  
  
<a name="ssSpecifier"></a>   
## <a name="the-ss-custom-format-specifier"></a>Identificatore di formato personalizzato "ss"  
 L'identificatore di formato personalizzato "ss" restituisce il valore della <xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType> proprietà, che rappresenta il numero di secondi interi nell'intervallo di tempo che non è incluso come parte del relativo ore, giorni o componente di minuti. Per valori compresi tra 0 e 9, la stringa di output include uno zero iniziale.  
  
 Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "ss" per interpretare la stringa numerica come numero di secondi. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#18)]
 [!code-vb[Conceptual.TimeSpan.Custom#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#18)]  
  
 Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "ss".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#19)]
 [!code-vb[Conceptual.TimeSpan.Custom#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#19)]  
  
 [Torna alla tabella](#table)  
  
<a name="fSpecifier"></a>   
## <a name="thef-custom-format-specifier"></a>L'identificatore di formato personalizzato "f"  
 L'identificatore di formato personalizzato "f" restituisce i decimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> (metodo), la stringa di input deve contenere esattamente una cifra frazionaria.  
  
 Se l'identificatore di formato personalizzato "f" viene usato da solo, specificare "%f" in modo che non venga interpretato erroneamente come stringa in formato standard.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "f" per visualizzare i decimi di secondo in un <xref:System.TimeSpan> valore. "f" viene usato prima come unico identificatore di formato e quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="ffSpecifier"></a>   
## <a name="the-ff-custom-format-specifier"></a>Identificatore di formato personalizzato "ff"  
 L'identificatore di formato personalizzato "ff" restituisce i centesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> (metodo), la stringa di input deve contenere esattamente due cifre frazionarie.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "ff" per visualizzare i centesimi di secondo in un <xref:System.TimeSpan> valore. "ff" viene usato prima come unico identificatore di formato, quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f3Specifier"></a>   
## <a name="the-fff-custom-format-specifier"></a>Identificatore di formato personalizzato "fff"  
 L'identificatore di formato personalizzato "fff" (con tre caratteri "f") restituisce i millisecondi in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> (metodo), la stringa di input deve contenere esattamente tre cifre frazionarie.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "fff" per visualizzare il numero di millisecondi in un <xref:System.TimeSpan> valore. "fff" viene usato prima come unico identificatore di formato e quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f4Specifier"></a>   
## <a name="the-ffff-custom-format-specifier"></a>Identificatore di formato personalizzato "ffff"  
 L'identificatore di formato personalizzato "ffff" (con quattro caratteri "f") restituisce i decimillesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> (metodo), la stringa di input deve contenere esattamente quattro cifre frazionarie.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "ffff" per visualizzare i decimillesimi di secondo in un <xref:System.TimeSpan> valore. "ffff" viene usato prima come unico identificatore di formato e quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f5Specifier"></a>   
## <a name="the-fffff-custom-format-specifier"></a>Identificatore di formato personalizzato "fffff"  
 L'identificatore di formato personalizzato "fffff" (con cinque caratteri "f") restituisce i centesimi di millesimo di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> (metodo), la stringa di input deve contenere esattamente cinque cifre frazionarie.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "fffff" per visualizzare i centomillesimi di secondo in un <xref:System.TimeSpan> valore. "fffff" viene usato prima come unico identificatore di formato e quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f6Specifier"></a>   
## <a name="the-ffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "ffffff"  
 L'identificatore di formato personalizzato "ffffff" (con sei caratteri "f") restituisce i milionesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> (metodo), la stringa di input deve contenere esattamente sei cifre frazionarie.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "ffffff" per visualizzare i milionesimi di secondo in un <xref:System.TimeSpan> valore. Viene usato prima come unico identificatore di formato, quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f7Specifier"></a>   
## <a name="the-fffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "fffffff"  
 L'identificatore di formato personalizzato "fffffff" (con sette caratteri "f") restituisce i decimilionesimi di secondo (o il numero frazionario di tick) in un intervallo di tempo. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> (metodo), la stringa di input deve contenere esattamente sette cifre frazionarie.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "fffffff" per visualizzare il numero di segni di graduazione frazionario un <xref:System.TimeSpan> valore. Viene usato prima come unico identificatore di formato, quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="F_Specifier"></a>   
## <a name="the-f-custom-format-specifier"></a>Identificatore di formato personalizzato "F"  
 L'identificatore di formato personalizzato "F" restituisce i decimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se il valore dei decimi di secondo dell'intervallo di tempo è zero, non viene incluso nella stringa del risultato. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> , la presenza di decimi di secondo cifra è facoltativa.  
  
 Se l'identificatore di formato personalizzato "F" viene usato da solo, specificare "%F" in modo che non venga interpretato erroneamente come stringa in formato standard.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "F" per visualizzare i decimi di secondo in un <xref:System.TimeSpan> valore. Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#21)]
 [!code-vb[Conceptual.TimeSpan.Custom#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#21)]  
  
 [Torna alla tabella](#table)  
  
<a name="FF_Specifier"></a>   
## <a name="the-ff-custom-format-specifier"></a>Identificatore di formato personalizzato "FF"  
 L'identificatore di formato personalizzato "FF" restituisce i centesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> , la presenza dei decimi e centesimi di secondo cifra sono facoltativi.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "FF" per visualizzare i centesimi di secondo in un <xref:System.TimeSpan> valore. Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#22)]
 [!code-vb[Conceptual.TimeSpan.Custom#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#22)]  
  
 [Torna alla tabella](#table)  
  
<a name="F3_Specifier"></a>   
## <a name="the-fff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFF"  
 L'identificatore di formato personalizzato "FFF" (con tre caratteri "F") restituisce i millisecondi in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> , la presenza di decimi, centesimi e i millesimi di una seconda cifra è facoltativa.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "FFF" per visualizzare i millesimi di secondo in un <xref:System.TimeSpan> valore. Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#23)]
 [!code-vb[Conceptual.TimeSpan.Custom#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#23)]  
  
 [Torna alla tabella](#table)  
  
<a name="F4_Specifier"></a>   
## <a name="the-ffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFF"  
 L'identificatore di formato personalizzato "FFFF" (con quattro caratteri "F") restituisce i decimillesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> , la presenza di decimi, centesimi, millesimi e decimillesimi di una seconda cifra è facoltativa.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "FFFF" per visualizzare i decimillesimi di secondo in un <xref:System.TimeSpan> valore. L'identificatore di formato personalizzato "FFFF" viene usato anche in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#24](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#24)]
 [!code-vb[Conceptual.TimeSpan.Custom#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#24)]  
  
 [Torna alla tabella](#table)  
  
<a name="F5_Specifier"></a>   
## <a name="the-fffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFFF"  
 L'identificatore di formato personalizzato "FFFFF" (con cinque caratteri "F") restituisce i centesimi di millesimo di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> , la presenza di decimi, centesimi, millesimi, decimillesimi e centomillesimi di una seconda cifra è facoltativa.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "FFFFF" per visualizzare i centomillesimi di secondo in un <xref:System.TimeSpan> valore. L'identificatore di formato personalizzato "FFFFF" viene usato anche in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#25](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#25)]
 [!code-vb[Conceptual.TimeSpan.Custom#25](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#25)]  
  
 [Torna alla tabella](#table)  
  
<a name="F6_Specifier"></a>   
## <a name="the-ffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFFFF"  
 L'identificatore di formato personalizzato "FFFFFF" (con sei caratteri "F") restituisce i milionesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> , la presenza di decimi, centesimi, millesimi, decimillesimi, centomillesimi e milionesimi di secondo cifra è facoltativa.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "FFFFFF" per visualizzare i milionesimi di secondo in un <xref:System.TimeSpan> valore. Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#26](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#26)]
 [!code-vb[Conceptual.TimeSpan.Custom#26](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#26)]  
  
 [Torna alla tabella](#table)  
  
<a name="F7_Specifier"></a>   
## <a name="the-fffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFFFFF"  
 L'identificatore di formato personalizzato "FFFFFFF" (con sette caratteri "F") restituisce i decimilionesimi di secondo (o il numero frazionario di tick) in un intervallo di tempo. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> , la presenza di sette cifre frazionarie nella stringa di input è facoltativa.  
  
 L'esempio seguente usa l'identificatore di formato personalizzato "FFFFFFF" per visualizzare le parti di frazioni di secondo in un <xref:System.TimeSpan> valore. Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#27](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#27)]
 [!code-vb[Conceptual.TimeSpan.Custom#27](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#27)]  
  
 [Torna alla tabella](#table)  
  
<a name="Other"></a>   
## <a name="other-characters"></a>Altri caratteri  
 Qualsiasi altro carattere senza codice di escape in una stringa di formato, incluso un carattere di spazio vuoto, viene interpretato come identificatore di formato personalizzato. Nella maggior parte dei casi, la presenza di eventuali altri senza caratteri di escape risultati carattere in un <xref:System.FormatException>.  
  
 È possibile includere un carattere letterale in una stringa di formato in due modi:  
  
-   Racchiudendolo tra virgolette singole (delimitatore di stringa letterale).  
  
-   Anteporvi una barra rovesciata ("\\"), che viene interpretato come carattere di escape. In C#, pertanto, la stringa di formato deve essere @-quoted o il carattere letterale deve essere preceduto da una barra rovesciata aggiuntiva.  
  
     In alcuni casi, potrebbe essere necessario utilizzare la logica condizionale per includere un valore letterale preceduto da una barra rovesciata in una stringa di formato. Nell'esempio seguente viene utilizzata la logica condizionale per includere un simbolo di segno per intervalli di tempo negativi.  
  
     [!code-csharp[Conceptual.TimeSpan.Custom#29](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/negativevalues1.cs#29)]
     [!code-vb[Conceptual.TimeSpan.Custom#29](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/negativevalues1.vb#29)]  
  
 In .NET non viene definita una grammatica per i separatori negli intervalli di tempo. I separatori tra giorni e ore, ore e minuti, minuti e secondi e secondi e frazioni di secondo devono pertanto essere trattati come valori letterali carattere in una stringa di formato.  
  
 Nell'esempio seguente vengono usati sia il carattere di escape che la virgoletta singola per definire una stringa di formato personalizzata che include la parola "minutes" nella stringa di output.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#28](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/literal1.cs#28)]
 [!code-vb[Conceptual.TimeSpan.Custom#28](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/literal1.vb#28)]  
  
 [Torna alla tabella](#table)  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)  
 [Stringhe di formato TimeSpan standard](../../../docs/standard/base-types/standard-timespan-format-strings.md)
