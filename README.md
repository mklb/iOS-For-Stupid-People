#iOS Dev. for Stupid People [Objective-C Edition]
Snippet collection of stupid things every iOS dev needs every day but keeps forgetting.. #copypaste4tw
Why? Because I don´t want to waste time anymore solving the same damn problems I already solved before and forgot.. #ginhelpsmeforgetstuff

##Table views & custom cells

### Without a xib file:
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

### With an xib file

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

##Table/Collection views & custom cells

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

### Always clean up!
We *always* use reusable cells in table/collection views! So clean up everything you added to the cell after init to prevent weird stuff!

```objective-c
-(void)prepareForReuse{
  // reset everything you added after init, for example:
  // [self.image removeFromSuperview];
  // self.image = nil;
}
```