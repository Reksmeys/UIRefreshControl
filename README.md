# UIRefreshControl

Implementing UIRefreshControl on TableViews in Swift 4 iOS 11 Xcode 9.2


 my few months of iOS learning, I have created many tableviews. However, I had never implemented an UIRefreshControl on a tableview, which is a control that sets of the refreshing of tableview contents.

ចំណាំ៖

A UIRefreshControl object provides a standard control that can be used to initiate the refreshing of a table view’s contents.
You link a refresh control to a table through an associated table view controller object. 
The table view controller handles the work of adding the control to the table’s visual appearance and managing 
the display of that control in response to appropriate user gestures. — Apple Documentation

- ការ Implement

import UIKit


class RefreshTableViewController: UITableViewController {
    
    @IBOutlet var foodTableView: UITableView!
    var refresh: UIRefreshControl!
    var dataTableArray = ["Chicken Soup","Beef Soup","Fried Chicken","Omelet"]
    override func viewDidLoad() {
        super.viewDidLoad()
        refresh = UIRefreshControl()
        foodTableView.addSubview(refresh)
        refresh.attributedTitle = NSAttributedString(string: "Pull to refresh")
        refresh.tintColor = UIColor.purple
        refresh.addTarget(self, action: #selector(didRefreshData), for: .valueChanged)
        

    }
    @objc func didRefreshData(){
        let otherArray = ["Roast Chicken", "Kimchi"]
        dataTableArray.append(contentsOf: otherArray)
        foodTableView.reloadData()
        refresh.endRefreshing()
    }


    // MARK: - Table view data source

    override func numberOfSections(in tableView: UITableView) -> Int {
        // #warning Incomplete implementation, return the number of sections
        return 1
    }

    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        // #warning Incomplete implementation, return the number of rows
        return dataTableArray.count
    }

    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)

        cell.textLabel?.text = dataTableArray[indexPath.row]

        return cell
    }
    

