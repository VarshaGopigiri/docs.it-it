---
title: Esplorazione di oggetti DataTable
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
ms.assetid: 202026a1-ec79-435e-b507-12a77f5011b2
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 2233beeab5bc613966375f9a8ccf18c333e9f4c6
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="navigating-datatables"></a>Esplorazione di oggetti DataTable
Il tipo <xref:System.Data.DataTableReader> presenta il contenuto di uno o più oggetti <xref:System.Data.DataTable> sotto forma di uno o più set di risultati forward-only di sola lettura.  
  
 Un tipo <xref:System.Data.DataTableReader> può contenere più set di risultati se viene creato tramite il metodo <xref:System.Data.DataSet.CreateDataReader%2A>. Quando è presente più di un set di risultati, il metodo <xref:System.Data.DataTableReader.NextResult%2A> sposta il cursore al set di risultati successivo. Questa proprietà è forward-only. Non è possibile tornare a un set di risultati precedente.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, il `TestConstructor` metodo crea due <xref:System.Data.DataTable> istanze. Per illustrare questo costruttore per il <xref:System.Data.DataTableReader> (classe), l'esempio crea un nuovo **DataTableReader** basato su una matrice che contiene i due **DataTable**ed esegue un'operazione semplice, stampa il contenuto delle prime colonne nella finestra della console.  
  
 [!code-csharp[DataWorks DataTableReader.NextResult#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTableReader.NextResult/CS/source.cs#1)]
 [!code-vb[DataWorks DataTableReader.NextResult#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTableReader.NextResult/VB/source.vb#1)]  
  
## <a name="see-also"></a>Vedere anche  
 [DataTableReader](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatablereaders.md)  
 [Provider gestiti ADO.NET e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
