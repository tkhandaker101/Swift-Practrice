#iOS Development Cheatsheet

TODO:
* [] Screenshots
* [] Videos

Note: In order to create your user interface Programmatically make sure withing your projects settings that Main Interface and the Launch Screen File are left blank. 
also...
* Navigate to project settings
* Under "App Icons and Launch Images" click on "Use Asset Catalog"
* Select "Migrate" on the popup that appears. make new Asset.

ViewController Template
```Swift
import UIKit

class ViewController: UIViewController {
    
    override func viewDidLoad() {
        super.viewDidLoad()
        self.view.backgroundColor=UIColor.whiteColor()
        
    }
    
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        
    }
}
```

UITabController Example

```Swift
import UIKit

class ViewController: UITabBarController {
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        addChildViewControllers()
        
        print(tabBar.subviews)
    }
    
    override func viewDidAppear(animated: Bool) {
        super.viewDidAppear(animated)

        setComposedBtn()
    }
    
    
    private func addChildViewControllers() {
        
        addChildViewController(TestViewController(), title: "Alarms", imageName: "alarm")
        
        addChildViewController(TestViewController(), title: "Sleep Alarm", imageName: "sleep")
        
        addChildViewController(TestViewController(), title: "", imageName: "add")
        
        addChildViewController(TestViewController(), title: "Awake Alarm", imageName: "awake")
        
        addChildViewController(TestViewController(), title: "Settings", imageName: "settings")
        
        // addChildViewController(UIViewController()) ~ Blank

    }
    
    private func addChildViewController(vc: UIViewController, title: String, imageName: String) {
        

        vc.title = title
        vc.tabBarItem.image = UIImage(named: imageName)
        

        let nav = UINavigationController(rootViewController: vc)
        addChildViewController(nav)
    }
    

    lazy private var composeBtn: UIButton = {
        

        let btn = UIButton()
        
        btn.setImage(UIImage(named: "tabbar_compose_icon_add"), forState: UIControlState.Normal)
        btn.setImage(UIImage(named: "tabbar_compose_icon_add_highlighted"), forState: UIControlState.Highlighted)
        
        btn.setBackgroundImage(UIImage(named: "tabbar_compose_button"), forState: UIControlState.Normal)
        btn.setBackgroundImage(UIImage(named: "tabbar_compose_button_highlighted"), forState: UIControlState.Highlighted)
        
        self.tabBar.addSubview(btn)
        
        btn.addTarget(self, action: "clickComposeBtn", forControlEvents: UIControlEvents.TouchUpInside)
        
        return btn
        }()
    
    private func setComposedBtn() {
        
        let w = tabBar.bounds.width / CGFloat(viewControllers!.count)
        let rect = CGRectMake(0, 0, w, tabBar.bounds.height)

        composeBtn.frame = CGRectOffset(rect, 2 * w, 0)
    }
    
    func clickComposeBtn() {
        print(__FUNCTION__)
    }
}
```

Variable Examples
```Swift
var nav: UINavigationController!
var window: UIWindow?
```

App Delegate Configuration
```Swift
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?
    var nav:UINavigationController?
    
    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
        
        
        var navigationBarAppearace = UINavigationBar.appearance()
        navigationBarAppearace.tintColor = UIColor.redColor()
        navigationBarAppearace.barTintColor = UIColor.redColor()
        navigationBarAppearace.titleTextAttributes = [NSForegroundColorAttributeName:UIColor.whiteColor()]
        
        UINavigationBar.appearance().barStyle = .BlackTranslucent
        UINavigationBar.appearance().tintColor = UIColor.whiteColor()
        
        
        self.window = UIWindow(frame: UIScreen.mainScreen().bounds)
        
        self.window!.backgroundColor = UIColor.whiteColor()
        self.window!.makeKeyAndVisible()
        
        var mainViewController: ViewController? = ViewController(nibName: nil, bundle: nil)
        self.nav = UINavigationController(rootViewController: mainViewController!)
        
        self.window!.rootViewController = self.nav
        self.nav!.setNavigationBarHidden(true, animated: false)
        return true
        
    }
```

Creating a Image Programmatically
```Swift

var imageView = UIImageView(frame: CGRectMake(20, 400, 100, 150));
var image = UIImage(named: "image.jpg");
imageView.image = image;
self.view.addSubview(imageView);

```

Creating a Circular Image (with a border)
```Swift
imageView.layer.cornerRadius = imageView.frame.size.width / 2
imageView.layer.borderColor = UIColor.whiteColor().CGColor
imageView.layer.borderWidth = 1.0
imageView.clipsToBounds = true
```

Creating a Label Programmatically
```Swift
        var label = UILabel(frame: CGRectMake(120, 80, 150, 100));
        label.center = CGPointMake(160, 284);
        label.textAlignment = NSTextAlignment.Center;
        label.text = "Hello, World!";
        label.numberOfLines=4;
        self.view.addSubview(label);
```

Creating a Button Programmatically
```Swift
        var button = UIButton(frame: CGRectMake(20, 20, 280, 40));
        button.backgroundColor=UIColor.blueColor();
        button.setTitle("Button Text", forState: .Normal);
        button.setTitleColor(UIColor.yellowColor(), forState: .Normal);
        button.alpha=0.6;
        button.layer.borderWidth=0.3;
        button.layer.cornerRadius=2;
        
        // Button Action
        // NOTE: "goToOtherViewController" is a function that performs what the button should do.
        
        button.addTarget(self, action: "goToOtherViewController", forControlEvents: .TouchUpInside);
        button.titleLabel!.textAlignment=NSTextAlignment.Center;
        self.view.addSubview(button);
```

Action Example (ViewController Redirection)
```Swift

    func goToOtherViewController(){
    
        self.navigationController!.pushViewController(secondViewController(), animated: false);
        
        }

```

Date Picker Programmatically
```Swift
        
        var datepick=UIDatePicker(frame:CGRectMake(20, 80, 280, 100));
        datepick.datePickerMode = UIDatePickerMode.Date;
        self.view.addSubview(datepick);
        
```
WebView Programmatically
```Swift
        var webview=UIWebView(frame:CGRectMake(20, 240, 280, 310));
        var url = NSURL(string: "https://twitter.com/migos");
        var request = NSURLRequest(URL: url!);
        webview.scalesPageToFit=true;
        webview.loadRequest(request);
        self.view.addSubview(webview);
```
CGRectMake Parameters
```Swift
CGRectMake(x, y, width, height)
```
Change status bar color (white) 
* Status bar style: UIStatusBarStyleLightContent
* View controller-based status bar appearance: NO
* Status bar is initially hidden: NO
Add this to your AppDelegate
```Swift
UIApplication.sharedApplication().statusBarStyle = UIStatusBarStyle.LightContent
```

Navigation Bar Tint Color
```Swift

nav.navigationBar.barTintColor = rgbaToUIColor(r: 52, g: 86, b: 121, a: 1.0)

```

Navigation Bar Text Color
```Swift
nav.navigationBar.titleTextAttributes = [UITextAttributeTextColor: UIColor.whiteColor()]
```

AlertView
```Swift
var alertView=UIAlertView();
alertView.title="Ayy Lmao";
alertView.addButtonWithTitle("K Then");
alertView.message="oh its lit";
alertView.show();
```

Label Size
```Swift
label.font = label.font.fontWithSize(20)
```

Set view background to a resource image
```Swift
self.view.backgroundColor = UIColor(patternImage: UIImage(named: "bg.jpg")!)
```

Adding a Navigation Bar
```Swift
import UIKit

class ViewController: UIViewController, UINavigationBarDelegate {
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
    }
    
    override func viewDidAppear(animated: Bool) {
        
        // Create the navigation bar
        let navigationBar = UINavigationBar(frame: CGRectMake(0, 20, self.view.frame.size.width, 44)) // Offset by 20 pixels vertically to take the status bar into account
        navigationBar.backgroundColor = UIColor.whiteColor()
        navigationBar.delegate = self;
        
        // Create a navigation item with a title
        let navigationItem = UINavigationItem()
        navigationItem.title = "Title"
        
        // Create left and right button for navigation item
        let leftButton = UIBarButtonItem(title: "Left", style: UIBarButtonItemStyle.Plain, target: self, action: nil)
        let rightButton = UIBarButtonItem(title: "Right", style: UIBarButtonItemStyle.Plain, target: self, action: nil)
        
        // Create two buttons for the navigation item
        navigationItem.leftBarButtonItem = leftButton
        navigationItem.rightBarButtonItem = rightButton
        
        // Assign the navigation item to the navigation bar
        navigationBar.items = [navigationItem]
        
        // Make the navigation bar a subview of the current view controller
        self.view.addSubview(navigationBar)
    }
    
    func positionForBar(bar: UIBarPositioning!) -> UIBarPosition {
        return UIBarPosition.TopAttached
    }
}
```

Some Pretty Colors
```Swift

extension UIColor {
    convenience init?(hex: String?){
        var rgbValue: CUnsignedLongLong = 0
        var scanner = NSScanner(string: hex!)
        if hex?.hasPrefix("#") == true {scanner.scanLocation = 1}
        scanner.scanHexLongLong(&rgbValue)
        var color = UIColor(red: CGFloat((rgbValue & 0xFF0000) >> 16)/255.0,
            green: CGFloat((rgbValue & 0x00FF00) >> 8)/255.0,
            blue: CGFloat(rgbValue & 0x0000FF)/255.0, alpha: 1.0)
        self.init(CGColor: color.CGColor)
    }
    var PSRed: UIColor          {return UIColor(hex: "#F44336")!}
    var PSPink: UIColor         {return UIColor(hex: "#E91E63")!}
    var PSPurple: UIColor       {return UIColor(hex: "#9C27B0")!}
    var PSDarkPurple: UIColor   {return UIColor(hex: "#673AB7")!}
    var PSIndigo: UIColor       {return UIColor(hex: "#3F51B5")!}
    var PSBlue: UIColor         {return UIColor(hex: "#2196F3")!}
    var PSCyan: UIColor         {return UIColor(hex: "#00BCD4")!}
    var PSTeal: UIColor         {return UIColor(hex: "#009688")!}
    var PSGreen: UIColor        {return UIColor(hex: "#4CAF50")!}
    var PSLightGreen: UIColor   {return UIColor(hex: "#8BC34A")!}
    var PSYellow: UIColor       {return UIColor(hex: "#FFEB3B")!}
    var PSLightOrange: UIColor  {return UIColor(hex: "#FFC107")!}
    var PSOrange: UIColor       {return UIColor(hex: "#FF9800")!}
    var PSDarkOrange: UIColor   {return UIColor(hex: "#FF5722")!}
    var PSBrown: UIColor        {return UIColor(hex: "#795548")!}
    var PSGrey: UIColor         {return UIColor(hex: "#9E9E9E")!}
    var PSLightGrey: UIColor    {return UIColor(hex: "#EEEEEE")!}
    var PSDarkGrey: UIColor     {return UIColor(hex: "#424242")!}
}

```
Usage (Example):
```Swift
UIColor().PSGreen
```