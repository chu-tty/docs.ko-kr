---
title: '방법: 뷰에서 데이터 필터링'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- views [WPF], filtering data
- filtering data in views [WPF]
- data binding [WPF], filtering data in views
ms.assetid: c76e8606-4cc4-45a8-9110-e2ec66dc6afd
ms.openlocfilehash: ea49897ca5e9cb6b639cf7d98ff05bd287c51761
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2019
ms.locfileid: "73453476"
---
# <a name="how-to-filter-data-in-a-view"></a>방법: 뷰에서 데이터 필터링
이 예제에서는 뷰에서 데이터를 필터링 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 필터를 만들려면 필터링 논리를 제공 하는 메서드를 정의 합니다. 메서드는 콜백으로 사용 되며 `object`형식의 매개 변수를 허용 합니다. 다음 메서드는 `filled` 속성이 "No"로 설정 된 모든 `Order` 개체를 반환 하 여 나머지 개체를 필터링 합니다.  
  
 [!code-csharp[SortFilter#2](~/samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#2)]
 [!code-vb[SortFilter#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#2)]  
  
 그런 다음, 다음 예제와 같이 필터를 적용할 수 있습니다. 이 예제에서 `myCollectionView`은 <xref:System.Windows.Data.ListCollectionView> 개체입니다.  
  
 [!code-csharp[SortFilter#Filter](~/samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#filter)]
 [!code-vb[SortFilter#Filter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#filter)]  
  
 필터링을 실행 취소 하려면 <xref:System.Windows.Data.CollectionView.Filter%2A> 속성을 `null`로 설정 하면 됩니다.  
  
 [!code-csharp[SortFilter#Unfilter](~/samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#unfilter)]
 [!code-vb[SortFilter#Unfilter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#unfilter)]  
  
 보기를 만들거나 가져오는 방법에 대 한 자세한 내용은 [데이터 컬렉션의 기본 뷰 가져오기](how-to-get-the-default-view-of-a-data-collection.md)를 참조 하세요. 전체 예제를 보려면 [뷰 샘플에서 항목 정렬 및 필터링](https://go.microsoft.com/fwlink/?LinkID=160040)을 참조 하세요.  
  
 뷰 개체가 <xref:System.Windows.Data.CollectionViewSource> 개체에서 제공 되는 경우 <xref:System.Windows.Data.CollectionViewSource.Filter> 이벤트에 대 한 이벤트 처리기를 설정 하 여 필터링 논리를 적용 합니다. 다음 예에서는 `listingDataView` <xref:System.Windows.Data.CollectionViewSource>의 인스턴스입니다.  
  
 [!code-csharp[DataBindingLab#10](~/samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#10)]
 [!code-vb[DataBindingLab#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#10)]  
  
 다음은 예제 `ShowOnlyBargainsFilter` 필터 이벤트 처리기의 구현을 보여 줍니다. 이 이벤트 처리기는 <xref:System.Windows.Data.FilterEventArgs.Accepted%2A> 속성을 사용 하 여 `CurrentPrice` $25 이상인 `AuctionItem` 개체를 필터링 합니다.  
  
 [!code-csharp[DataBindingLab#5](~/samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#5)]
 [!code-vb[DataBindingLab#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#5)]  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Data.CollectionView.CanFilter%2A>
- <xref:System.Windows.Data.BindingListCollectionView.CustomFilter%2A>
- [데이터 바인딩 개요](../../../desktop-wpf/data/data-binding-overview.md)
- [뷰의 데이터 정렬](how-to-sort-data-in-a-view.md)
- [방법 항목](data-binding-how-to-topics.md)
