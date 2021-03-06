---
title: 'Procedura: eseguire direttamente query SQL'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: e491b9bf-741a-4296-9f51-76c25ddf6a82
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 000a7c50edacbae09675a9f9069f56aa6cd211f6
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="how-to-directly-execute-sql-queries"></a>Procedura: eseguire direttamente query SQL
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] le query create vengono convertite in query SQL con parametri, in formato testo, e inviate al server SQL per l'elaborazione.  
  
 Non è possibile eseguire in SQL la varietà di metodi eventualmente disponibili localmente per l'applicazione, pertanto [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tenta di convertire questi metodi locali nelle operazioni e funzioni equivalenti disponibili nell'ambiente SQL. Per la maggior parte dei metodi e degli operatori nei tipi [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] incorporati sono disponibili conversioni dirette in comandi SQL. Alcuni possono essere prodotti dalle funzioni disponibili. Quelli che non possono essere prodotti generano eccezioni in fase di esecuzione. Per ulteriori informazioni, vedere [Mapping dei tipi CLR SQL](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md).  
  
 Nei casi in cui una query [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fosse insufficiente per un'attività specializzata, è possibile usare il metodo <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> per eseguire una query SQL, quindi convertire direttamente il risultato della query in oggetti.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente si supponga che i dati per la classe `Customer` siano distribuiti in due tabelle (customer1 e customer2). La query consente di restituire una sequenza di oggetti `Customer`.  
  
 [!code-csharp[DLinqQuerying#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#4)]
 [!code-vb[DLinqQuerying#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#4)]  
  
 Purché i nomi di colonna nei risultati tabulari corrispondano alle proprietà di colonna della classe di entità, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] crea gli oggetti da qualsiasi query SQL.  
  
## <a name="example"></a>Esempio  
 Il metodo <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> accetta anche parametri. Per eseguire una query con parametri, usare codice analogo al seguente:  
  
 [!code-csharp[DLinqQuerying#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#5)]
 [!code-vb[DLinqQuerying#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#5)]  
  
 I parametri sono espressi nel testo della query usando la stessa notazione con parentesi graffe usata da `Console.WriteLine()` e `String.Format()`. In effetti, `String.Format()` viene infatti chiamato nella stringa di query specificata, sostituendo i parametri tra parentesi graffe con nomi di parametro generati, ad esempio @p0, @p1 ..., @p(n).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di base](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)  
 [Esecuzione di query sul database](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)
