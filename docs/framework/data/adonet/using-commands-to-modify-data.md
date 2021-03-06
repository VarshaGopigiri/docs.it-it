---
title: Utilizzo di comandi per modificare i dati
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 70a83453eef990a03515a4860917f3c4d72599c3
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="using-commands-to-modify-data"></a>Utilizzo di comandi per modificare i dati
Con un provider di dati .NET Framework è possibile eseguire stored procedure o istruzioni DDL (Data Definition Language), ad esempio CREATE TABLE e ALTER COLUMN, per modificare lo schema di un database o di un catalogo. Questi comandi non restituiscono righe come una query, pertanto la **comando** oggetto fornisce un **ExecuteNonQuery** per elaborarli.  
  
 Oltre a utilizzare **ExecuteNonQuery** per modificare lo schema, è inoltre possibile utilizzare questo metodo per elaborare le istruzioni SQL che modificano i dati ma che non restituiscono righe, ad esempio INSERT, UPDATE e DELETE.  
  
 Anche se le righe non vengono restituite dal **ExecuteNonQuery** parametri di metodo di input e output e valori restituiti possono essere passati e restituiti tramite il **parametri** insieme del **comando**  oggetto.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Aggiornamento di dati in un'origine dati](../../../../docs/framework/data/adonet/updating-data-in-a-data-source.md)  
 Viene descritto come eseguire i comandi o le stored procedure che modificano i dati in un database.  
  
 [Esecuzione di operazioni di catalogo](../../../../docs/framework/data/adonet/performing-catalog-operations.md)  
 Viene descritto come eseguire i comandi per la modifica dello schema di database.  
  
## <a name="see-also"></a>Vedere anche  
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)  
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)  
 [Provider gestiti ADO.NET e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
