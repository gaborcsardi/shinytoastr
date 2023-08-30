
# shinytoastr

> Notifications in Shiny, via [toastr](https://github.com/CodeSeven/toastr)

[![Project Status: Active - The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)
[![R-CMD-check](https://github.com/gaborcsardi/shinytoastr/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/gaborcsardi/shinytoastr/actions/workflows/R-CMD-check.yaml)
[![](https://www.r-pkg.org/badges/version/shinytoastr)](https://www.r-pkg.org/pkg/shinytoastr)
[![CRAN RStudio mirror downloads](https://cranlogs.r-pkg.org/badges/shinytoastr)](https://www.r-pkg.org/pkg/shinytoastr)

<h1 align="center">
    <img width="400" src="./inst/shinytoastr.png">
</h1>

## Installation

```r
source("https://install-github.me/gaborcsardi/shinytoastr")
```

## Usage

Call `useToastr()` at the beginning of `ui` definition, and then
in the `server` definition use one of the notification functions,
`toastr_success()`, `toastr_info()`, `toastr_warning()` or
`toastr_error()` to create notifications:

```r
library(shinytoastr)

ui <- shinyUI(fluidPage(
  useToastr(),
  pageWithSidebar(
    headerPanel("Header"),
    sidebarPanel(
	  ...
      actionButton(inputId = "save_button", label = "Save",
	                class = "btn-primary")
      ...
    ),
    mainPanel(
      ...
    )
  )
))
```

```r
server <- function(input, output, session) {
  ...
  observeEvent(
    input$save_button,
    {
      tryCatch(
        {
          writeToDB(data)
          toastr_success("Saved to database")
        },
        error = function(e) {
          toastr_error(title = "Database error", conditionMessage(e))
        }
      )
    }
  )
}
```

## License

MIT © John Papa, Tim Ferrell, Hans Fjällemark,
[Mango Solutions](https://github.com/mangothecat), Posit Software, PBC.
