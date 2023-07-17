[[2023-04-21]]

## Problem
`UICollectionViewDiffableDataSource` przyjmuje jako parametr `cellProvider`, który miał referencje do delegatów (`weak var` we właścicielach) powodujące cykle zależności.

___
## Sprawa
Szymon T. odezwał się do mnie w ciekawej sprawie dotyczącej *retain cycle*:
```
private lazy var dataSource = EDCreateVariableIntervalSummaryDataSource(
	collectionView: collectionView,
	deleteDelegate: self,  
	addIntervalButtonHandler: interactor?.addInterval,  
	copyIntervalHandler: { [weak self] presentable in
		self?.unswipeCells(self?.collectionView.visibleCells ?? []) 
		self?.interactor?.didTapCopyInterval(presentable)`  
	},  
	cellReorderDelegate: self, 
	reorderDelegate: interactor)
```

> Ten wycinek kodu pochodzi z jednego z ViewControllerow, wychodzi na to, ze strong reference jest tutaj miedzy ViewControllerem ktory ma ten wlasnie dataSource i samym dataSource a powoduja go dwa delegaty:` deleteDelegate:` `self,` oraz  `cellReorderDelegate:` `self`, po wykomentowaniu delegatow memory leaks nie zachodzi. ponizej kawalek codu z clasy  `EDCreateVariableIntervalSummaryDataSource`:`final**` `**class**` `EDCreateVariableIntervalSummaryDataSource: UICollectionViewDiffableDataSource<`  
`String,`  
`EDCreateVariableIntervalSummaryCellPresentable`  
`> {`  
`**weak**` `**var**` `reorderDelegate: EDCreateVariableIntervalSummaryReorderDelegate?`  
  
`**init**``(collectionView: UICollectionView,`  
`deleteDelegate: EDDeletableCollectionCellDelegate,`  
`addIntervalButtonHandler: (() -> Void)?,`  
`copyIntervalHandler: ((EDCreateVariableIntervalSummaryCellPresentable) -> Void)?,`  
`cellReorderDelegate: EDCreateVariableIntervalSummaryCellReorderDelegate?,`  
`reorderDelegate: EDCreateVariableIntervalSummaryReorderDelegate?) {`  
`**super**``.init(`  
`collectionView: collectionView,`  
`cellProvider: { collectionView, indexPath, presentable -> UICollectionViewCell?` `**in**`  
`**let**` `cell = collectionView.dequeueReusableCell(`  
`withReuseIdentifier: R.reuseIdentifier.edCreateVariableIntervalSummaryCell,`  
`for: indexPath)`  
`cell?.setupWith(`  
`presentable: presentable,`  
`copyHandler: copyIntervalHandler)`  
`cell?.deleteDelegate = deleteDelegate`  
`cell?.reorderDelegate = cellReorderDelegate`  
  
`**return**` `cell`  
`})`

> podejrzewam, ze dodanie `[weak self]` tutaj: `cellProvider: { [weak self] collectionView, indexPath, presentable -> UICollectionViewCell?` `**in**`  
**zalatwiloby sprawe ale tak nie mozna bo leci error:** `**s**``elf' used before 'super.init' call`tutaj wlasnie mam ten problem, jak to najlepiej rozegrac?

## Rozwiązanie
```
[weak deleteDelegate, weak cellReorderDelegate] collectionView, indexPath, presentable in
```

Skoro nie możemy złapać `self`, to może złapmy słabo parametry?
___
Zadziałało ✅