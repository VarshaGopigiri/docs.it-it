---
title: Sintassi di markup del percorso
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attribute usage in XAML [WPF]
- XAML [WPF], attribute usage
- graphics [WPF], PathGeometry class
- XAML [WPF], object element usage
ms.assetid: b8586241-a02d-486e-9223-e1e98e047f41
caps.latest.revision: "22"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 9cd8f9b14f114060ebec8e336c1212d61fa19c83
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="path-markup-syntax"></a>Sintassi di markup del percorso
Vengono descritti i percorsi in [forme e disegno di base di WPF Overview](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md) e [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md), tuttavia, in questo argomento descrive in dettaglio il potente e complesso mini linguaggio consente di specificare percorso in modo più compatto usando le geometrie [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>Prerequisiti  
 Per comprendere questo argomento, è necessario conoscere le funzionalità di base di <xref:System.Windows.Media.Geometry> oggetti. Per ulteriori informazioni, vedere il [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
<a name="abouthisdocument"></a>   
## <a name="streamgeometry-and-pathfigurecollection-mini-languages"></a>Mini linguaggi StreamGeometry e PathFigureCollection  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]sono disponibili due classi che forniscono mini lingue per la descrizione di percorsi geometrici: <xref:System.Windows.Media.StreamGeometry> e <xref:System.Windows.Media.PathFigureCollection>.  
  
-   Utilizzare il <xref:System.Windows.Media.StreamGeometry> lingue ridotto durante l'impostazione di una proprietà di tipo <xref:System.Windows.Media.Geometry>, ad esempio il <xref:System.Windows.UIElement.Clip%2A> proprietà di un <xref:System.Windows.UIElement> o <xref:System.Windows.Shapes.Path.Data%2A> proprietà di un <xref:System.Windows.Shapes.Path> elemento. L'esempio seguente usa la sintassi degli attributi per creare un <xref:System.Windows.Media.StreamGeometry>.  
  
     [!code-xaml[GeometrySample_snip_XAML#GraphicsMMStreamGeometryAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmstreamgeometryattributesyntaxinline)]  
  
-   Utilizzare il <xref:System.Windows.Media.PathFigureCollection> lingue ridotto durante l'impostazione di <xref:System.Windows.Media.PathGeometry.Figures%2A> proprietà di un <xref:System.Windows.Media.PathGeometry>. L'esempio seguente usa una sintassi di attributo per creare un <xref:System.Windows.Media.PathFigureCollection> per un <xref:System.Windows.Media.PathGeometry>.  
  
     [!code-xaml[GeometrySample_snip_XAML#GraphicsMMPathFigureCollectionAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmpathfigurecollectionattributesyntaxinline)]  
  
 Come si può notare dagli esempi precedenti, i due mini-linguaggi sono molto simili. È sempre possibile usare un <xref:System.Windows.Media.PathGeometry> in qualsiasi situazione in cui è possibile utilizzare un <xref:System.Windows.Media.StreamGeometry>; pertanto quello che è necessario utilizzare? Utilizzare un <xref:System.Windows.Media.StreamGeometry> quando non è necessario modificare il percorso dopo averlo creato; utilizzare un <xref:System.Windows.Media.PathGeometry> se è necessario modificare il percorso.  
  
 Per ulteriori informazioni sulle differenze tra <xref:System.Windows.Media.PathGeometry> e <xref:System.Windows.Media.StreamGeometry> degli oggetti, vedere il [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
### <a name="a-note-about-white-space"></a>Nota sugli spazi vuoti  
 Per brevità nelle sezioni di sintassi seguenti viene illustrato uno spazio singolo, ma sono accettabili più spazi quando viene visualizzato uno spazio singolo.  
  
 Non è necessario che due numeri siano separati da virgole o spazi vuoti, ma ciò può essere fatto solo quando la stringa risultante è ambigua. Ad esempio, `2..3` è composta da due numeri: "2". e ".3". Analogamente, `2-3` è "2" e "-3". Gli spazi non sono necessari né prima né dopo i comandi.  
  
### <a name="syntax"></a>Sintassi  
 Il [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] attributo sintassi di utilizzo di un <xref:System.Windows.Media.StreamGeometry> è costituito da un parametro facoltativo <xref:System.Windows.Media.FillRule> valore e uno o più descrizioni di figure.  
  
|Utilizzo degli attributi XAML StreamGeometry|  
|-----------------------------------------|  
|`<`*oggetto* *proprietà* `="`[ `fillRule`] `figureDescription`[ `figureDescription`] *`" ... />`|  
  
 Il [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] attributo sintassi di utilizzo di un <xref:System.Windows.Media.PathFigureCollection> è costituito da uno o più descrizioni di figure.  
  
|Utilizzo degli attributi XAML PathFigureCollection|  
|-----------------------------------------------|  
|`<`*oggetto* *proprietà* `="` `figureDescription`[ `figureDescription`] *`" ... />`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*fillRule*|<xref:System.Windows.Media.FillRule?displayProperty=nameWithType><br /><br /> Specifica se il <xref:System.Windows.Media.StreamGeometry> utilizza il <xref:System.Windows.Media.FillRule.EvenOdd> o <xref:System.Windows.Media.FillRule.Nonzero> <xref:System.Windows.Media.PathGeometry.FillRule%2A>.<br /><br /> -   `F0`Specifica il <xref:System.Windows.Media.FillRule.EvenOdd> regola di riempimento.<br />-   `F1`Specifica il <xref:System.Windows.Media.FillRule.Nonzero> regola di riempimento.<br /><br /> Se si omette questo comando, il sottopercorso utilizza il comportamento predefinito, ovvero <xref:System.Windows.Media.FillRule.EvenOdd>. Se si specifica questo comando, è necessario inserirlo per primo.|  
|*figureDescription*|Figura costituita da un comando di spostamento, da alcuni comandi di disegno e da un comando di chiusura facoltativo.<br /><br /> `moveCommand` `drawCommands`  `[` `closeCommand` `]`|  
|*moveCommand*|Comando di spostamento che specifica il punto iniziale della figura. Vedere il [comando Sposta](#themovecommand) sezione.|  
|*drawCommands*|Uno o più comandi di disegno che descrivono il contenuto della figura. Vedere il [comandi Draw](#drawcommands) sezione.|  
|*closeCommand*|Comando facoltativo di chiusura che consente di chiudere la figura. Vedere il [comando Chiudi](#closecommand) sezione.|  
  
<a name="themovecommand"></a>   
## <a name="move-command"></a>Comando Move  
 Specifica il punto iniziale di una nuova figura.  
  
|Sintassi|  
|------------|  
|`M` *startPoint*<br /><br /> -oppure-<br /><br /> `m` *startPoint*|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*startPoint*|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto iniziale di una nuova figura.|  
  
 Maiuscoli `M` indica che `startPoint` è un valore assoluto; una minuscola `m` indica che `startPoint` è un offset al punto precedente, oppure (0,0) se non esiste. Se dopo il comando di spostamento vengono elencati più punti, verrà tracciata una linea in direzione di quei punti, anche se il comando della linea è stato specificato.  
  
<a name="drawcommands"></a>   
## <a name="draw-commands"></a>Comandi Draw  
 Un comando di disegno può essere costituito da diversi comandi di forma. Sono disponibili i comandi di forma seguenti: linea, linea orizzontale, linea verticale, curva di Bézier cubica, curva di Bézier quadratica, curva di Bézier cubica continua, curva di Bézier quadratica continua e arco ellittico.  
  
 Per inserire ciascun comando, usare una lettera maiuscola o una lettera minuscola: le lettere maiuscole indicano valori assoluti, quelle minuscole valori relativi. I punti di controllo del segmento specificato si riferiscono al punto finale dell'esempio precedente. Quando si immette in sequenza più comandi dello stesso tipo, è possibile omettere la voce di comando duplicato. ad esempio, `L 100,200 300,400` equivale a `L 100,200 L 300,400`. Nella tabella seguente vengono descritti il **spostare** e **disegnare** comandi.  
  
### <a name="line-command"></a>Comando Line  
 Crea una linea retta tra il punto corrente e il punto finale specificato. `l 20 30`e `L 20,30` sono esempi di valido **riga** comandi.  
  
|Sintassi|  
|------------|  
|`L` *endPoint*<br /><br /> -oppure-<br /><br /> `l` *endPoint*|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*endPoint*|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto finale della linea.|  

Maiuscoli `L` indica che `endPoint` è un valore assoluto; una minuscola `l` indica che `endPoint` è un offset al punto precedente, oppure (0,0) se non esiste.

### <a name="horizontal-line-command"></a>Comando Horizontal Line  
 Crea una linea orizzontale tra il punto corrente e la coordinata x specificata. `H 90` è un esempio di comando di linea orizzontale valido.

  
|Sintassi|  
|------------|  
|`H`  *x*<br /><br /> -oppure-<br /><br /> `h`  *x*|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*x*|<xref:System.Double?displayProperty=nameWithType><br /><br /> Coordinata x del punto finale della linea.|  
  
Maiuscoli `H` indica che `x` è un valore assoluto; una minuscola `h` indica che `x` è un offset al punto precedente, oppure (0,0) se non esiste.
  
### <a name="vertical-line-command"></a>Comando Vertical Line  
 Crea una linea verticale tra il punto corrente e la coordinata y specificata. `v 90` è un esempio di comando di linea verticale valido.

  
|Sintassi|  
|------------|  
|`V`  *y*<br /><br /> -oppure-<br /><br /> `v`  *y*|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*y*|<xref:System.Double?displayProperty=nameWithType><br /><br /> Coordinata y del punto finale della linea.|  

Maiuscoli `V` indica che `y` è un valore assoluto; una minuscola `v` indica che `y` è un offset al punto precedente, oppure (0,0) se non esiste.  
    
### <a name="cubic-bezier-curve-command"></a>Comando Cubic Bezier Curve  
 Crea una curva di Bézier cubica tra il punto corrente e il punto finale specificato utilizzando i due punti di controllo (`controlPoint`1 e `controlPoint`2). `C 100,200 200,400 300,200` è un esempio di comando di curva valido.  
  
|Sintassi|  
|------------|  
|`C` `controlPoint`1`controlPoint`2`endPoint`<br /><br /> -oppure-<br /><br /> `c` `controlPoint`1`controlPoint`2`endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`controlPoint`1|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Primo punto di controllo della curva, che determina la tangente iniziale della curva.|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Secondo punto di controllo della curva, che determina la tangente finale della curva.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto verso il quale viene disegnata la curva.|  
  
### <a name="quadratic-bezier-curve-command"></a>Comando Quadratic Bezier Curve  
 Crea una curva di Bézier quadratica tra il punto corrente e il punto finale specificato utilizzando il punto di controllo (`controlPoint`). `q 100,200 300,200` è un esempio di comando di curva di Bézier quadratica valido.  
  
|Sintassi|  
|------------|  
|`Q` `controlPoint` `endPoint`<br /><br /> -oppure-<br /><br /> `q` `controlPoint` `endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto di controllo della curva, che determina le tangenti iniziale e finale della curva.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto verso il quale viene disegnata la curva.|  
  
### <a name="smooth-cubic-bezier-curve-command"></a>Comando Smooth cubic Bezier curve  
 Crea una curva di Bézier cubica tra il punto corrente e il punto finale specificato. Il primo punto di controllo viene considerato come reflection del secondo punto di controllo del comando precedente relativo al punto corrente. Se in precedenza non è stato usato alcun comando o se il comando precedente non era un comando di curva di Bézier cubica o un comando di curva di Bézier cubica continua, il punto di controllo coinciderà con il punto corrente. Il secondo punto di controllo, il punto di controllo per la fine della curva, specificato da `controlPoint`2. Ad esempio, `S 100,200 200,300` è un comando di curva di Bézier cubico continua valido.  
  
|Sintassi|  
|------------|  
|`S` `controlPoint`2`endPoint`<br /><br /> -oppure-<br /><br /> `s` `controlPoint`2`endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto di controllo della curva, che determina la tangente finale della curva.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto verso il quale viene disegnata la curva.|  
  
### <a name="smooth-quadratic-bezier-curve-command"></a>Comando Smooth Quadratic Bezier Curve  
 Crea una curva di Bézier quadratica tra il punto corrente e il punto finale specificato. Il punto di controllo viene considerato come reflection del punto di controllo del comando precedente relativo al punto corrente. Se in precedenza non è stato usato alcun comando o se il comando precedente non era un comando di curva di Bézier quadratica o un comando di curva di Bézier quadratica continua, il punto di controllo coinciderà con il punto corrente.  
  
|Sintassi|  
|------------|  
|`T` `controlPoint` `endPoint`<br /><br /> -oppure-<br /><br /> `t` `controlPoint` `endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto di controllo della curva, che determina l'inizio e la tangente della curva.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto verso il quale viene disegnata la curva.|  
  
### <a name="elliptical-arc-command"></a>Comando Elliptical Arc  
 Crea un arco ellittico tra il punto corrente e il punto finale specificato.  
  
|Sintassi|  
|------------|  
|`A` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`<br /><br /> -oppure-<br /><br /> `a` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`size`|<xref:System.Windows.Size?displayProperty=nameWithType><br /><br /> Raggio x e raggio y dell'arco.|  
|`rotationAngle`|<xref:System.Double?displayProperty=nameWithType><br /><br /> Rotazione dell'ellisse in gradi.|  
|`isLargeArcFlag`|Impostato su 1 se la misura dell'angolo dell'arco deve essere di 180 gradi o superiore. In caso contrario, impostato su 0.|  
|`sweepDirectionFlag`|Impostato su 1 se l'arco viene tracciato nella direzione di un angolo positivo. In caso contrario, impostato su 0.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> Punto verso cui viene disegnata l'arco.|  
  
<a name="closecommand"></a>   
## <a name="the-close-command"></a>Comando Close  
 Termina la figura corrente e crea una linea che collega il punto corrente e il punto iniziale della figura. Questo comando crea una giunzione di linee (angolo) tra l'ultimo segmento e il primo segmento della figura.  
  
|Sintassi|  
|------------|  
|`Z`<br /><br /> -oppure-<br /><br /> `z`|  

<a name="pointsyntax"></a>   
## <a name="point-syntax"></a>Sintassi del punto  
 Descrive le coordinate x e y di un punto in cui (0,0) è l'angolo superiore sinistro.
  
|Sintassi|  
|------------|  
|`x` `,` `y`<br /><br /> -oppure-<br /><br /> `x` `y`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`x`|<xref:System.Double?displayProperty=nameWithType><br /><br /> Coordinata x del punto.|  
|`y`|<xref:System.Double?displayProperty=nameWithType><br /><br /> Coordinata y del punto.|  
  
<a name="specialvalues"></a>   
## <a name="special-values"></a>Valori speciali  
 Anziché un valore numerico standard, è anche possibile usare i valori speciali seguenti. Per questi valori viene effettuata la distinzione tra maiuscole e minuscole.  
  
 Infinito  
 Rappresenta <xref:System.Double.PositiveInfinity?displayProperty=nameWithType>.  
  
 -Infinito  
 Rappresenta <xref:System.Double.NegativeInfinity?displayProperty=nameWithType>.  
  
 NaN  
 Rappresenta <xref:System.Double.NaN?displayProperty=nameWithType>.  
  
 È anche possibile usare una notazione scientifica. Ad esempio, `+1.e17` è un valore valido.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Shapes.Path>  
 <xref:System.Windows.Media.StreamGeometry>  
 <xref:System.Windows.Media.PathGeometry>  
 <xref:System.Windows.Media.PathFigureCollection>  
 [Cenni preliminari sugli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)  
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)  
 [Procedure relative alle proprietà](../../../../docs/framework/wpf/graphics-multimedia/geometries-how-to-topics.md)
