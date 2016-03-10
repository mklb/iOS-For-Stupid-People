#iOS Dev. for Stupid People [Objective-C Edition]
Snippet collection of stupid things every iOS dev needs every day but keeps forgetting.. #copypaste4tw
Why? Because I don´t want to waste time anymore solving the same damn problems I already solved before and forgot.. #ginhelpsmeforgetstuff

##Table views & custom cells

### Without a xib file:
```objective-c
// Register cell
// tableviewcontroller.m
[self.tableView registerClass:[AwseomeCellClass class] forCellReuseIdentifier:reuseIdentifier];

// customization of the cell
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