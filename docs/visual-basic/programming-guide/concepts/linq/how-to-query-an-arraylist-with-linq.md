---
title: 'Procedura: eseguire Query di ArrayList con LINQ (Visual Basic)'
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 176358a9-d765-4b57-9557-7feb4428138d
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 6740d8a7c6d4a31ccd3730249695c24c6417785d
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-query-an-arraylist-with-linq-visual-basic"></a>Procedura: eseguire Query di ArrayList con LINQ (Visual Basic)
Quando si usa LINQ per eseguire una query su raccolte <xref:System.Collections.IEnumerable> non generiche, ad esempio <xref:System.Collections.ArrayList>, è necessario dichiarare in modo esplicito il tipo della variabile di intervallo in base al tipo specifico di oggetti nella raccolta. Ad esempio, se dispone di un <xref:System.Collections.ArrayList> di `Student` oggetti, il [dalla clausola](../../../../visual-basic/language-reference/queries/from-clause.md) dovrebbe essere simile al seguente:  
  
```  
Dim query = From student As Student In arrList   
...  
```  
  
 Specificando il tipo della variabile di intervallo, si esegue il cast di ogni elemento di <xref:System.Collections.ArrayList> in `Student`.  
  
 L'uso di una variabile di intervallo tipizzata in modo esplicito in un'espressione di query è equivalente alla chiamata del metodo <xref:System.Linq.Enumerable.Cast%2A>. <xref:System.Linq.Enumerable.Cast%2A> genera un'eccezione se non è possibile eseguire il cast specificato. <xref:System.Linq.Enumerable.Cast%2A> e <xref:System.Linq.Enumerable.OfType%2A> sono i due metodi dell'operatore query standard che operano sui tipi <xref:System.Collections.IEnumerable> non generici. In Visual Basic, è necessario chiamare esplicitamente il <xref:System.Linq.Enumerable.Cast%2A> metodo nell'origine dei dati per assicurare un tipo di variabile di intervallo specifico. Per ulteriori informazioni, vedere[relazioni tra i tipi nelle operazioni di Query (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md).  
  
## <a name="example"></a>Esempio  
 L'esempio seguente mostra una query semplice su un oggetto <xref:System.Collections.ArrayList>. Si noti che questo esempio usa gli inizializzatori di oggetto quando il codice chiama il metodo <xref:System.Collections.ArrayList.Add%2A>, anche se non si tratta di un requisito.  
  
```vb  
Imports System.Collections  
Imports System.Linq  
  
Module Module1  
  
    Public Class Student  
        Public Property FirstName As String  
        Public Property LastName As String  
        Public Property Scores As Integer()  
    End Class  
  
    Sub Main()  
  
        Dim student1 As New Student With {.FirstName = "Svetlana",   
                                     .LastName = "Omelchenko",   
                                     .Scores = New Integer() {98, 92, 81, 60}}  
        Dim student2 As New Student With {.FirstName = "Claire",   
                                    .LastName = "O'Donnell",   
                                    .Scores = New Integer() {75, 84, 91, 39}}  
        Dim student3 As New Student With {.FirstName = "Cesar",   
                                    .LastName = "Garcia",   
                                    .Scores = New Integer() {97, 89, 85, 82}}  
        Dim student4 As New Student With {.FirstName = "Sven",   
                                    .LastName = "Mortensen",   
                                    .Scores = New Integer() {88, 94, 65, 91}}  
  
        Dim arrList As New ArrayList()  
        arrList.Add(student1)  
        arrList.Add(student2)  
        arrList.Add(student3)  
        arrList.Add(student4)  
  
        ' Use an explicit type for non-generic collections  
        Dim query = From student As Student In arrList   
                    Where student.Scores(0) > 95   
                    Select student  
  
        For Each student As Student In query  
            Console.WriteLine(student.LastName & ": " & student.Scores(0))  
        Next  
        ' Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
  
End Module  
' Output:  
'   Omelchenko: 98  
'   Garcia: 97  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
