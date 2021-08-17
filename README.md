# Prompt

Prompt for cli apps. Currently in development, use with care.

## Use

```Go
var p *promt.Prompt
var selection string

selFn = func(item interface{}) error {
		selection = fmt.Sprintf("%s", item)
		p.Stop()
		return nil
	}

infoFn = func(item interface{}) [][]term.Cell {
	i := term.Cprint("WARNING: this operation cannot be undone", color.FgRed)
	return [][]term.Cell{i}
}

p = prompt.Create("Question", &prompt.Options{LineSize: 5}, []string{"yes", "no"},
 prompt.WithSelectionHandler(sel), prompt.WithInformation(infoFn))

err = p.Run(context.Background())
if err != nil {
	return err
}

fmt.Printf("%s is selected\n", selection)
```