#iOS Dev. for Stupid People Objective-C Edition
Snippet collection of stupid things every iOS dev needs every day but keeps forgetting.. #copypaste4tw
Why? Because I don´t want to waste time anymore solving the same damn problems I already solved before and forgot.. #ginhelpsmeforgetstuff

##Table views & custom cells

### Without a xib file:
```objective-c
// Register cell
// tableviewcontroller.m
[self.tableView registerClass:[AwseomeCellClass class] forCellReuseIdentifier:reuseIdentifier];

// customisatin of the cell
// cell.m
- (id)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier{
    self = [super initWithStyle:style reuseIdentifier:reuseIdentifier];
    if (self) {
        
    }
    
    return self;
}
```

### With an xib file
```objective-c
// register cell
// tableviewcontroller.m
[self.tableView registerNib:[UINib nibWithNibName:reuseIdentifier bundle:nil] forCellReuseIdentifier:reuseIdentifier];

// customisatin of the cell
// cell.m
- (void)awakeFromNib:
```