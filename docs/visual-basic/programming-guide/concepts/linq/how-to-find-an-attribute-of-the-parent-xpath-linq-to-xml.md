---
title: 'Procedura: trovare un attributo dell''elemento padre (XPath-LINQ to XML) (Visual Basic)'
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9d2572fd-27d4-426c-b079-16854cb9ec7d
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 4da7888ab838dacbdda097f24580745692d407fd
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-find-an-attribute-of-the-parent-xpath-linq-to-xml-visual-basic"></a>Procedura: trovare un attributo dell'elemento padre (XPath-LINQ to XML) (Visual Basic)
In questo argomento viene illustrato come spostarsi all'elemento padre e trovare un relativo attributo.  
  
 L'espressione XPath è:  
  
 `../@id`  
  
## <a name="example"></a>Esempio  
 Viene innanzitutto individuato un elemento `Author`. Quindi, viene individuato l'attributo `id` dell'elemento padre.  
  
 Questo esempio usa il documento XML seguente: [File XML di esempio: libri (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-books-linq-to-xml.md).  
  
```vb  
Dim books As XDocument = XDocument.Load("Books.xml")  
Dim author As XElement = books.Root.<Book>.<Author>.FirstOrDefault()  
  
' LINQ to XML query  
Dim att1 As XAttribute = author.Parent.Attribute("id")  
  
' XPath expression  
Dim att2 As XAttribute = DirectCast(author.XPathEvaluate("../@id"),  _  
    IEnumerable).Cast(Of XAttribute)().First()  
  
If att1 Is att2 Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
Console.WriteLine(att1)  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Results are identical  
id="bk101"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to XML per gli utenti di XPath (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
