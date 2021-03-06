### Migration guide: MDCAppBar to MDCAppBarViewController

`MDCAppBarViewController` is a direct replacement for `MDCAppBar`. The migration essentially looks
like so:

```swift
// Step 1
-  let appBar = MDCAppBar()
+  let appBarViewController = MDCAppBarViewController()

// Step 2
-  self.addChildViewController(appBar.headerViewController)
+  self.addChildViewController(appBarViewController)

// Step 3
-  appBar.addSubviewsToParent()
+  view.addSubview(appBarViewController.view)
+  appBarViewController.didMove(toParentViewController: self)
```

`MDCAppBarViewController` is a subclass of `MDCFlexibleHeaderViewController`, meaning you configure
an `MDCAppBarViewController` instance exactly the same way you'd configure an
`MDCFlexibleHeaderViewController` instance.

`MDCAppBar` also already uses `MDCAppBarViewController` under the hood so you can directly replace
any references of `appBar.headerViewController` with `appBarViewController`.

#### Swift find and replace recommendations

| Find | Replace |
|:-----|:-------------|
| `let appBar = MDCAppBar()` | `let appBarViewController = MDCAppBarViewController()` |
| `self.addChildViewController(appBar.headerViewController)` | `self.addChildViewController(appBarViewController)` |
| `appBar.addSubviewsToParent()` | `view.addSubview(appBarViewController.view)`<br/>`appBarViewController.didMove(toParentViewController: self)` |
| `self.appBar.headerViewController` | `self.appBarViewController` |

#### Objective-C find and replace recommendations

| Find | Replace |
|:-----|:-------------|
| `MDCAppBar *appBar;` | `MDCAppBarViewController *appBarViewController;` |
| `appBar = [[MDCAppBar alloc] init]` | `appBarViewController = [[MDCAppBarViewController alloc] init]` |
| `addChildViewController:appBar.headerViewController` | `addChildViewController:appBarViewController` |
| `[self.appBar addSubviewsToParent];` | `[self.view addSubview:self.appBarViewController.view];`<br/>`[self.appBarViewController didMoveToParentViewController:self];` |

#### Example migrations

- [MDCCatalog examples](https://github.com/material-components/material-components-ios/commit/50e1fd091d8d08426f390c124bf6310c54174d8c)
