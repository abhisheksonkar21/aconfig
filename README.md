package main

import (
	"log"
	"github.com/yourusername/aconfig" // Replace with actual import path
	"github.com/yourusername/aconfigyaml" // Replace with actual import path
)

type MyConfig struct {
	Port int `default:"1111" usage:"just give a number"`
	Auth struct {
		User string `required:"true"`
		Pass string `required:"true"`
	}
	Pass string `default:"" env:"SECRET" flag:"sec_ret"`
}

func main() {
	var cfg MyConfig

	loader := aconfig.LoaderFor(&cfg, aconfig.Config{
		// feel free to skip some steps :)
		// SkipDefaults: true,
		// SkipFiles:    true,
		// SkipEnv:      true,
		// SkipFlags:    true,
		EnvPrefix:    "APP",
		FlagPrefix:   "app",
		Files: []string{
			"/var/opt/myapp/config.json",
			"ouch.yaml",
		},
		FileDecoders: map[string]aconfig.FileDecoder{
			// from `aconfigyaml` submodule
			// see submodules in repo for more formats
			".yaml": aconfigyaml.New(),
		},
	})

	// IMPORTANT: define your own flags with `flagSet`
	flagSet := loader.Flags()

	if err := loader.Load(); err != nil {
		log.Fatalf("Error loading config: %v", err)
	}

	// Configuration fields will be loaded from (in order):
	// 1. defaults set in structure tags (see MyConfig definition)
	// 2. loaded from files (config.json, then ouch.yaml)
	// 3. from corresponding environment variables with the prefix `APP_`
	// 4. command-line flags with the prefix `app.`
}



***^ Use this code in place of that 
and change the web chromedriver to new patch ^***
