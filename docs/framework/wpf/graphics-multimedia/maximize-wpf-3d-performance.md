---
title: Ottimizzazione delle prestazioni tridimensionali di WPF
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: 3-D graphics [WPF]
ms.assetid: 4bcf949d-d92f-4d8d-8a9b-1e4c61b25bf6
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 45053762a4782544531a09c92531b26f99663016
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="maximize-wpf-3d-performance"></a>Ottimizzazione delle prestazioni tridimensionali di WPF
Quando si utilizza il [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] per compilare controlli 3D e includere scene 3D nelle applicazioni, è importante prendere in considerazione l'ottimizzazione delle prestazioni. In questo argomento fornisce un elenco di classi e proprietà che hanno implicazioni sulle prestazioni dell'applicazione, insieme a indicazioni per l'ottimizzazione delle prestazioni quando vengono utilizzati in 3D.  
  
 Questo argomento si presuppone una conoscenza approfondita di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] funzionalità 3D. I suggerimenti in questo documento si applicano a "il rendering di livello 2", generalmente definito hardware che supporta la versione 2.0 del pixel shader e vertex shader versione 2.0. Per ulteriori informazioni, vedere [livelli per il Rendering di grafica](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md).  
  
## <a name="performance-impact-high"></a>Impatto sulle prestazioni: elevata  
  
|Proprietà|Consiglio|  
|-|-|  
|<xref:System.Windows.Media.Brush>|Velocità del pennello (veloce alla più lenta):<br /><br /> <xref:System.Windows.Media.SolidColorBrush><br /><br /> <xref:System.Windows.Media.LinearGradientBrush><br /><br /> <xref:System.Windows.Media.ImageBrush><br /><br /> <xref:System.Windows.Media.DrawingBrush>(cache)<br /><br /> <xref:System.Windows.Media.VisualBrush>(cache)<br /><br /> <xref:System.Windows.Media.RadialGradientBrush><br /><br /> <xref:System.Windows.Media.DrawingBrush>(non memorizzato nella cache)<br /><br /> <xref:System.Windows.Media.VisualBrush>(non memorizzato nella cache)|  
|<xref:System.Windows.UIElement.ClipToBoundsProperty>|Impostare `Viewport3D.ClipToBounds` su false quando non è necessario disporre di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] in modo esplicito ritagliare il contenuto di un <xref:System.Windows.Controls.Viewport3D> al rettangolo di Viewport3D. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]il ritaglio di anti-aliasing può essere molto lento, e `ClipToBounds` è abilitato (lento) per impostazione predefinita su <xref:System.Windows.Controls.Viewport3D>.|  
|<xref:System.Windows.UIElement.IsHitTestVisible%2A>|Impostare `Viewport3D.IsHitTestVisible` su false quando non è necessario [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] da prendere in considerazione il contenuto di un <xref:System.Windows.Controls.Viewport3D> quando si esegue il mouse hit test.  Hit test del contenuto 3D viene eseguito nel software e può essere lenta con mesh di grandi dimensioni. <xref:System.Windows.UIElement.IsHitTestVisible%2A>abilitato (lento) per impostazione predefinita su <xref:System.Windows.Controls.Viewport3D>.|  
|<xref:System.Windows.Media.Media3D.GeometryModel3D>|Creare modelli diversi solo quando sono necessari materiali o trasformazioni diverse.  In caso contrario, tentare di unire molti <xref:System.Windows.Media.Media3D.GeometryModel3D> istanze con lo stesso materiali e trasformazioni in alcune dimensioni maggiori <xref:System.Windows.Media.Media3D.GeometryModel3D> e <xref:System.Windows.Media.Media3D.MeshGeometry3D> istanze.|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|Animazione mesh, la modifica dei singoli vertici di una rete di base per frame: non è sempre efficiente in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  Per ridurre al minimo l'impatto sulle prestazioni di notifiche di modifica quando viene modificata ogni vertice, disconnettere la mesh dall'albero visuale prima di eseguire la modifica di ogni vertice.  Una volta la mesh è stata modificata, collegarlo all'albero visuale.  Inoltre, provare a ridurre le dimensioni di trame con cui verrà aggiunta un'animazione in questo modo.|  
|Anti-aliasing 3D|Per aumentare la velocità di rendering, disabilitare il campionamento multiplo su un <xref:System.Windows.Controls.Viewport3D> impostando la proprietà associata <xref:System.Windows.Media.RenderOptions.EdgeMode%2A> a `Aliased`.  Per impostazione predefinita, in è disabilitato anti-aliasing 3D [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] e attivato sul [!INCLUDE[TLA#tla_longhorn](../../../../includes/tlasharptla-longhorn-md.md)] con 4 campioni per pixel.|  
|Testo|Il testo attivo in una scena 3D (attivo perché si trova un <xref:System.Windows.Media.DrawingBrush> o <xref:System.Windows.Media.VisualBrush>) può richiedere molto tempo. Provare a utilizzare invece le immagini del testo (tramite <xref:System.Windows.Media.Imaging.RenderTargetBitmap>) a meno che non verrà modificato il testo.|  
|<xref:System.Windows.Media.TileBrush>|Se è necessario utilizzare un <xref:System.Windows.Media.VisualBrush> o <xref:System.Windows.Media.DrawingBrush> in una scena 3D poiché il contenuto del pennello non è statico, provare la memorizzazione nella cache il pennello (impostando la proprietà associata <xref:System.Windows.Media.RenderOptions.CachingHint%2A> a `Cache`).  Impostare le soglie di invalidamento di scala minima e massima (con le proprietà associate <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMinimum%2A> e <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A>) in modo che i pennelli memorizzati nella cache non essere rigenerati troppo spesso, pur mantenendo il livello desiderato di qualità.  Per impostazione predefinita, <xref:System.Windows.Media.DrawingBrush> e <xref:System.Windows.Media.VisualBrush> non vengono memorizzate, vale a dire che ogni volta che un elemento di disegno con pennello deve essere eseguito il rendering, l'intero contenuto del pennello deve innanzitutto essere nuovamente visualizzato in una superficie intermedia.|  
|<xref:System.Windows.Media.Effects.BitmapEffect>|<xref:System.Windows.Media.Effects.BitmapEffect>forza tutto il contenuto interessato da sottoporre a rendering senza l'accelerazione hardware.  Per prestazioni ottimali, non utilizzare <xref:System.Windows.Media.Effects.BitmapEffect>.|  
  
## <a name="performance-impact-medium"></a>Impatto sulle prestazioni: Media  
  
|Proprietà|Consiglio|  
|-|-|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|Quando una trama viene definita come triangoli adiacenti con vertici condivisi e i quali hanno la stessa posizione, normale e le coordinate di trama, definire ogni vertice condiviso una sola volta e quindi definire i triangoli in base all'indice con <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A>.|  
|<xref:System.Windows.Media.ImageBrush>|Provare a ridurre le dimensioni della trama quando si dispone di un controllo esplicito sulla dimensione (quando si utilizza un <xref:System.Windows.Media.Imaging.RenderTargetBitmap> e/o un <xref:System.Windows.Media.ImageBrush>).  Si noti che le trame risoluzione inferiore può ridurre la qualità visiva, pertanto provare a trovare il giusto equilibrio tra qualità e prestazioni.|  
|Opacità|Quando si esegue il rendering 3D semitrasparente contenuto (ad esempio i riflessi), utilizzare le proprietà di opacità su pennelli o materiali (tramite <xref:System.Windows.Media.Brush.Opacity%2A> o <xref:System.Windows.Media.Media3D.DiffuseMaterial.Color%2A>) invece di creare un apposito semitrasparente <xref:System.Windows.Controls.Viewport3D> impostando `Viewport3D.Opacity` su un valore minore di 1.|  
|<xref:System.Windows.Controls.Viewport3D>|Ridurre al minimo il numero di <xref:System.Windows.Controls.Viewport3D> gli oggetti in uso in una scena.  Inserire più modelli 3D il Viewport3D stesso, anziché la creazione di istanze di Viewport3D separate per ogni modello.|  
|<xref:System.Windows.Freezable>|In genere è utile riutilizzare <xref:System.Windows.Media.Media3D.MeshGeometry3D>, <xref:System.Windows.Media.Media3D.GeometryModel3D>, pennelli e materiali.  Tutti sono multiparentable poiché sono derivati da `Freezable`.|  
|<xref:System.Windows.Freezable>|Chiamare il <xref:System.Windows.Freezable.Freeze%2A> metodo sugli oggetti Freezable quando le proprietà rimangono invariate nell'applicazione.  Il blocco può diminuire working set e aumentare la velocità.|  
|<xref:System.Windows.Media.Brush>|Utilizzare <xref:System.Windows.Media.ImageBrush> anziché <xref:System.Windows.Media.VisualBrush> o <xref:System.Windows.Media.DrawingBrush> non cambierà quando il contenuto del pennello.  Il contenuto 2D può essere convertito in un <xref:System.Windows.Controls.Image> tramite <xref:System.Windows.Media.Imaging.RenderTargetBitmap> e usato in un <xref:System.Windows.Media.ImageBrush>.|  
|<xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A>|Non utilizzare <xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A> a meno che non sia effettivamente necessario vedere le facce degli indietro il <xref:System.Windows.Media.Media3D.GeometryModel3D>.|  
|<xref:System.Windows.Media.Media3D.Light>|Velocità della luce (veloce alla più lenta):<br /><br /> <xref:System.Windows.Media.Media3D.AmbientLight><br /><br /> <xref:System.Windows.Media.Media3D.DirectionalLight><br /><br /> <xref:System.Windows.Media.Media3D.PointLight><br /><br /> <xref:System.Windows.Media.Media3D.SpotLight>|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|Tenta di mantenere le dimensioni di trama in tali limiti:<br /><br /> <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A>: 20.001 <xref:System.Windows.Media.Media3D.Point3D> istanze<br /><br /> <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A>: 60.003 <xref:System.Int32> istanze|  
|<xref:System.Windows.Media.Media3D.Material>|Velocità del materiale (veloce alla più lenta):<br /><br /> <xref:System.Windows.Media.Media3D.EmissiveMaterial><br /><br /> <xref:System.Windows.Media.Media3D.DiffuseMaterial><br /><br /> <xref:System.Windows.Media.Media3D.SpecularMaterial>|  
|<xref:System.Windows.Media.Brush>|[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]3D non rifiutare esplicitamente i pennelli invisibili (pennelli per luce nere, deselezionare i pennelli e così via) in modo coerente.  Prendere in considerazione ometterli dalla scena.|  
|<xref:System.Windows.Media.Media3D.MaterialGroup>|Ogni <xref:System.Windows.Media.Media3D.Material> in un <xref:System.Windows.Media.Media3D.MaterialGroup> fa sì che un altro passaggio di rendering, pertanto l'inclusione di numerosi materiali, anche semplici, può aumentare moltissimo le richieste di riempimento alla GPU.  Ridurre al minimo il numero di oggetti Material nella <xref:System.Windows.Media.Media3D.MaterialGroup>.|  
  
## <a name="performance-impact-low"></a>Impatto sulle prestazioni: basso  
  
|Proprietà|Consiglio|  
|-|-|  
|<xref:System.Windows.Media.Media3D.Transform3DGroup>|Quando non è necessario l'animazione o l'associazione dati, anziché utilizzare un gruppo di trasformazione che contiene più trasformazioni, utilizzano un singolo <xref:System.Windows.Media.Media3D.MatrixTransform3D>, impostandolo come il prodotto di tutte le trasformazioni che altrimenti sarebbe infatti disponibile in modo indipendente nel gruppo di trasformazione.|  
|<xref:System.Windows.Media.Media3D.Light>|Ridurre al minimo il numero di luci nella scena. Un numero eccessivo di luci in una scena impone [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] eseguire il fallback al rendering software.  I limiti sono approssimativamente 110 <xref:System.Windows.Media.Media3D.DirectionalLight> oggetti, 70 <xref:System.Windows.Media.Media3D.PointLight> oggetti o 40 <xref:System.Windows.Media.Media3D.SpotLight> oggetti.|  
|<xref:System.Windows.Media.Media3D.ModelVisual3D>|Separare lo spostamento di oggetti da oggetti statici inserendoli in separata <xref:System.Windows.Media.Media3D.ModelVisual3D> istanze.  ModelVisual3D è "maggiore" <xref:System.Windows.Media.Media3D.GeometryModel3D> poiché memorizza nella cache i limiti trasformati.  GeometryModel3D è ottimizzato per essere un modello. ModelVisual3D è ottimizzato per essere un nodo della scena.  Utilizzare ModelVisual3D per inserire le istanze condivise di GeometryModel3D nella scena.|  
|<xref:System.Windows.Media.Media3D.Light>|Ridurre al minimo il numero di volte in cui che si modifica il numero di luci nella scena.  Ogni modifica del conteggio chiaro forza una rigenerazione dello shader e la ricompilazione, a meno che tale configurazione è disponibile in precedenza (e pertanto era relativo shader memorizzato nella cache).|  
|Chiaro|Luci nero non saranno visibili, ma vengono aggiunte in fase di rendering. prendere in considerazione ometterle.|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|Per ridurre al minimo il tempo di creazione di raccolte di grandi dimensioni in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], ad esempio un MeshGeometry3D <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A>, <xref:System.Windows.Media.Media3D.MeshGeometry3D.Normals%2A>, <xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A>, e <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A>, ridimensionare le raccolte prima della compilazione dei valori. Se possibile, passare costruttori prepopolato strutture di dati delle raccolte, ad esempio matrici o elenchi.|  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)
