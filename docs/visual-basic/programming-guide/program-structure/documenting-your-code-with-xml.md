---
title: Documentazione del codice tramite XML (Visual Basic)
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- XML [Visual Basic], documenting code
- XML comments, Visual Basic
- Visual Basic code, documenting with XML
ms.assetid: a0d35dc7-c5f9-4d74-92ff-a1c6f28d5235
caps.latest.revision: "17"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: ddb1f366002c4f0c675c591d83aab1b31ef8f602
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="documenting-your-code-with-xml-visual-basic"></a>Documentazione del codice tramite XML (Visual Basic)
In [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)], è possibile documentare il codice tramite XML  
  
## <a name="xml-documentation-comments"></a>Commenti relativi alla documentazione XML  
 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)]fornisce un modo semplice per creare automaticamente la documentazione XML per i progetti. È possibile generare automaticamente uno scheletro XML per i tipi e membri e quindi fornire i riepiloghi, documentazione descrittiva per ogni parametro e altre note. Con il programma di installazione appropriato, la documentazione XML viene generata automaticamente in un file XML con lo stesso nome del progetto e l'estensione XML. Per altre informazioni, vedere [/doc](../../../visual-basic/reference/command-line-compiler/doc.md).  
  
 Il file XML può essere utilizzato o manipolazione come XML. Questo file si trova nella stessa directory del file di .exe o DLL di output del progetto.  
  
 Documentazione XML inizia con `'''`. L'elaborazione di questi commenti presenta alcune restrizioni:  
  
-   La documentazione deve essere in codice XML ben formato. Se il codice XML non è corretto, viene generato un avviso e il file di documentazione contiene un commento per informare che si è verificato un errore.  
  
-   Gli sviluppatori sono liberi di creare set di tag personalizzati. È un set di tag (vedere "Sezioni correlate" in questo argomento). Alcuni tag consigliati hanno un significato speciale:  
  
    -   Il tag \< viene usato per descrivere i parametri. Se usato, il compilatore verifica che il parametro esista e che tutti i parametri siano descritti nella documentazione. Se la verifica ha esito negativo, il compilatore genera un avviso.  
  
    -   L'attributo `cref` può essere associato a qualsiasi tag per fornire un riferimento a un elemento del codice. Il compilatore verifica l'esistenza di questo elemento di codice. Se la verifica ha esito negativo, il compilatore genera un avviso. Il compilatore rispetta inoltre eventuali `Imports` istruzioni durante la ricerca di un tipo di `cref` attributo.  
  
    -   Il \<riepilogo > tag è utilizzato da IntelliSense nel [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] per visualizzare informazioni aggiuntive su un tipo o membro.  
  
## <a name="related-sections"></a>Sezioni correlate  
 Per informazioni dettagliate sulla creazione di un file XML con i commenti della documentazione, vedere gli argomenti seguenti:  
  
-   [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)  
  
-   [Tag di commento XML](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)  
  
-   [Elaborazione del file XML](../../../visual-basic/programming-guide/program-structure/processing-the-xml-file.md)  
  
-   [Procedura: Creare documentazione XML](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)  
  
-   [Strumenti XML in Visual Studio](/visualstudio/xml-tools/xml-tools-in-visual-studio)  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di applicazioni con Visual Basic](../../../visual-basic/developing-apps/index.md)  
 [Guida per programmatori Visual Basic](../../../visual-basic/programming-guide/index.md)
