# collectionViewExample

```swift
import UIKit

class MainVC: UIViewController {
    
    var rowNumber = 1
    
    @IBOutlet var contactCollectionView: UICollectionView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        contactCollectionView.reloadData()
        }
    
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        if segue.identifier == "toInfoPage" {
            let destination = segue.destination as! ContactInfoVC
            destination.rowNumber = rowNumber
        }
    }
}

extension MainVC: UICollectionViewDataSource {
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return contacts.contactsArray.count
    }
    
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let Cell = collectionView.dequeueReusableCell(withReuseIdentifier: "collectionCell", for: indexPath) as! ContactInfoListCollectionViewCell
        Cell.contactInfoLabel.text = contacts.contactsArray[indexPath.row].name
        return Cell
    }
}

extension MainVC: UICollectionViewDelegateFlowLayout {
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
        return CGSize(width: 188, height: 188)
    }
}

extension MainVC: UICollectionViewDelegate {
    func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath) {
     rowNumber = indexPath.row
        DispatchQueue.main.asyncAfter(deadline: .now() + 0.2) {
            self.performSegue(withIdentifier: "toInfoPage", sender: nil)
        }
    }
}
