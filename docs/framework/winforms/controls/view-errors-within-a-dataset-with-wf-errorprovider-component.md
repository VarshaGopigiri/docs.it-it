---
title: 'Procedura: visualizzare errori in un dataset tramite il componente ErrorProvider di Windows Form'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- errors [Windows Forms], dataset errors
- error messages [Windows Forms], viewing in datasets
- ErrorProvider component [Windows Forms], dataset errors
ms.assetid: cbae023f-d651-4210-bdea-bcc5f037e321
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 27ef4200996108e378273c5f813106d4f82dacd8
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-view-errors-within-a-dataset-with-the-windows-forms-errorprovider-component"></a>Procedura: visualizzare errori in un dataset tramite il componente ErrorProvider di Windows Form
È possibile utilizzare Windows Form <xref:System.Windows.Forms.ErrorProvider> componente per visualizzare gli errori di colonna all'interno di un set di dati o un'altra origine dati. Per un <xref:System.Windows.Forms.ErrorProvider> componente per visualizzare gli errori di dati in un form, non deve essere associata direttamente a un controllo. Una volta è associato a un'origine dati, è possibile visualizzare un'icona di errore accanto a qualsiasi controllo associato alla stessa origine dati.  
  
> [!NOTE]
>  Se si modifica il provider di errore <xref:System.Windows.Forms.ErrorProvider.DataSource%2A> e <xref:System.Windows.Forms.ErrorProvider.DataMember%2A> proprietà in fase di esecuzione, è consigliabile utilizzare il <xref:System.Windows.Forms.ErrorProvider.BindToDataAndErrors%2A> metodo per evitare conflitti.  
  
### <a name="to-display-data-errors"></a>Per visualizzare gli errori di dati  
  
1.  Associare il componente a una colonna specifica all'interno di una tabella di dati.  
  
    ```vb  
    ' Assumes existence of DataSet1, DataTable1  
    TextBox1.DataBindings.Add("Text", DataSet1, "Customers.Name")  
    ErrorProvider1.DataSource = DataSet1  
    ErrorProvider1.DataMember = "Customers"  
    ```  
  
    ```csharp  
    // Assumes existence of DataSet1, DataTable1  
    textBox1.DataBindings.Add("Text", DataSet1, "Customers.Name");  
    errorProvider1.DataSource = DataSet1;  
    errorProvider1.DataMember = "Customers";  
    ```  
  
2.  Impostare il <xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A> proprietà al form.  
  
    ```vb  
    ErrorProvider1.ContainerControl = Me  
    ```  
  
    ```csharp  
    errorProvider1.ContainerControl = this;  
    ```  
  
3.  Impostare la posizione del record corrente a una riga che contiene un errore di colonna.  
  
    ```vb  
    DataTable1.Rows(5).SetColumnError("Name", "Bad data in this row.")  
    Me.BindingContext(DataTable1).Position = 5  
    ```  
  
    ```csharp  
    DataTable1.Rows[5].SetColumnError("Name", "Bad data in this row.");  
    this.BindingContext [DataTable1].Position = 5;  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica sul componente ErrorProvider](../../../../docs/framework/winforms/controls/errorprovider-component-overview-windows-forms.md)  
 [Procedura: Visualizzare le icone di errori per la convalida dei form con il componente ErrorProvider di Windows Form](../../../../docs/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider.md)
