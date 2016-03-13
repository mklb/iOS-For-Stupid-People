#iOS Dev. for Stupid People [Objective-C Edition]
Snippet collection of stupid things every iOS dev needs every day but keeps forgetting.. #copypaste4tw
Why? Because I don´t want to waste time anymore solving the same damn problems I already solved before and forgot.. #ginhelpsmeforgetstuff

## Table/Collection views & custom cells

### Table View Without a xib file:
```objective-c
// Register cell
// tableviewcontroller.m
[self.tableView registerClass:[AwseomeCellClass class] forCellReuseIdentifier:reuseIdentifier];

// customization of a cell
// cell.m
- (id)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier{
    self = [super initWithStyle:style reuseIdentifier:reuseIdentifier];
    if (self) {
        // just be awesome and implement something here
    }
    
    return self;
}
```

### Table with an xib file

*First:* Set the reuseIdentifier in your xib file. xib file > Attributes Inspector

*Pro tip:* The reuseIdentifier should be the class name

```objective-c
// register cell
// tableviewcontroller.m
[self.tableView registerNib:[UINib nibWithNibName:reuseIdentifier bundle:nil] forCellReuseIdentifier:reuseIdentifier];

// customization of the cell
// cell.m
- (void)awakeFromNib{
  // customize me!
}
```

### Collection without a xib file:
```objective-c
// Register cell
// CollectionViewController.m
[self.collectionview registerClass:[AwseomeCellClass class] forCellWithReuseIdentifier:cellReuseIdentifier];

// customization of a cell
// cell.m
-(id)initWithFrame:(CGRect)frame{
    self = [super initWithFrame:frame];
    
    if (self) {
        // do stuff here
    }

    return self;
}
```

### Collection with an xib file

*First:* Set the reuseIdentifier in your xib file. xib file > Attributes Inspector

*Pro tip:* The reuseIdentifier should be the class name

```objective-c
// register cell
// CollectionViewController.m
[self.collectionview registerNib:[UINib nibWithNibName:cellReuseIdentifier bundle:nil]  forCellWithReuseIdentifier:cellReuseIdentifier];

// customization of the cell
// cell.m
- (void)awakeFromNib{
  // customize me!
}
```

### Good to know
We *always* use reusable cells in table/collection views! So clean up everything you added to the cell after init to prevent weird stuff!

```objective-c
-(void)prepareForReuse{
  // reset everything you added after init, for example:
  // [self.image removeFromSuperview];
  // self.image = nil;
}
```

Other nice stuff:
```objective-c
// tableViewController.m
// define the reuse identifier above the @interface
static NSString * const reuseIdentifier = @"CellClassName";
// hide cell separator
self.tableView.separatorColor = [UIColor clearColor];
// hide scrollbar
[self.tableView setShowsVerticalScrollIndicator:NO];

// cell.m
// prevent cell from selection highlighting
self.selectionStyle = UITableViewCellSelectionStyleNone;
```

##Images
```objective-c
// load an image from the asset catalog
UIImageView *image = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"AssetCatalogFileName"]];
// make an image round
image.layer.masksToBounds = true;
image.layer.cornerRadius = image.frame.size.width/2;
```

##Status bar

```objective-c
// Hide statusbar: "Status bar is initially hidden" YES or
// "View controller-based status bar appearance" YES and
// put this in every view controller
-(BOOL)prefersStatusBarHidden{
    return YES;
}
// Note: If you just want to hide the status bar just in your launch screen: "Status bar is initially hidden" YES and call prefersStatusBarHidden with false in your controllers (which is the default, so you don´t need to call anything..)

// Style statusbar

//  "View controller-based status bar appearance" NO
// AppDelegate.m
[[UIApplication sharedApplication] setStatusBarStyle:UIStatusBarStyleLightContent];
// "View controller-based status bar appearance" YES 
// in your first controlelr
[self.navigationController.navigationBar setBarStyle:UIBarStyleBlackTranslucent];
// or in every controller
- (UIStatusBarStyle)preferredStatusBarStyle
{ 
    return UIStatusBarStyleLightContent; 
}
```

## UINavigationBar
### Transparent UINavigationBar
```objective-c
// For tableviews/collectionviews: correct the top inset if you want
[self setAutomaticallyAdjustsScrollViewInsets:false];
self.extendedLayoutIncludesOpaqueBars = true;

// style the navigation bar transparent
// style for the whole app use: UINavigationBar *navigationBar = [UINavigationBar appearance];
[self.navigationController.navigationBar setBackgroundImage:[UIImage new]
                                              forBarMetrics:UIBarMetricsDefault];
self.navigationController.navigationBar.shadowImage = [UIImage new];
self.navigationController.navigationBar.translucent = YES;
self.navigationController.navigationBar.tintColor = [UIColor whiteColor];
```

### UINavigationBar with a logo (image)
```objective-c
// viewDidLoad method
// Your logo will resize perfectly, just edit YOUR_IMG_WIDTH_HERE
UIView *titleView =[[UIView alloc] initWithFrame:CGRectMake(0, 0, YOUR_IMG_WIDTH_HERE, 40)];
UIImageView *titleImageView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"logo"]];
titleImageView.frame = CGRectMake(0, 0,titleView.frame.size.width , titleView.frame.size.height);
[titleView addSubview:titleImageView];
titleImageView.contentMode = UIViewContentModeScaleAspectFit;
self.navigationItem.titleView = titleView;
```

## Effects
### iPhone movement caused effects with the Gyroscope
```objective-c
// motion effect x axis
UIInterpolatingMotionEffect *motionEffect = [[UIInterpolatingMotionEffect alloc] initWithKeyPath:@"center.x" type:UIInterpolatingMotionEffectTypeTiltAlongHorizontalAxis];
// or motion effect y axis
UIInterpolatingMotionEffect *motionEffect = [[UIInterpolatingMotionEffect alloc] initWithKeyPath:@"center.y" type:UIInterpolatingMotionEffectTypeTiltAlongVerticalAxis];
// min and max values
motionEffect.minimumRelativeValue = @(-YOUR_VALUE);
motionEffect.maximumRelativeValue = @(YOUR_VALUE);
[self.YOUR_VIEW addMotionEffect:motionEffect];
```