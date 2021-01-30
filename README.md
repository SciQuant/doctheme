# Documentation theme for the packages of SciQuant

*(requires at least documenter `v0.24.6`)*

Add the following before the `makedocs` command:

```julia
using DocumenterTools: Themes
# download the themes
for file in ("sciquant-lightdefs.scss", "sciquant-darkdefs.scss", "sciquant-style.scss")
    download("https://raw.githubusercontent.com/JuliaDynamics/doctheme/master/$file", joinpath(@__DIR__, file))
end
# create the themes
for w in ("light", "dark")
    header = read(joinpath(@__DIR__, "sciquant-style.scss"), String)
    theme = read(joinpath(@__DIR__, "sciquant-$(w)defs.scss"), String)
    write(joinpath(@__DIR__, "sciquant-$(w).scss"), header*"\n"*theme)
end
# compile the themes
Themes.compile(joinpath(@__DIR__, "sciquant-light.scss"), joinpath(@__DIR__, "src/assets/themes/documenter-light.css"))
Themes.compile(joinpath(@__DIR__, "sciquant-dark.scss"), joinpath(@__DIR__, "src/assets/themes/documenter-dark.css"))
```

Lastly, because we are using Google fonts, use
```julia
format = Documenter.HTML(
    assets = [
        asset("https://fonts.googleapis.com/css?family=Lato|Source+Code+Pro&display=swap", class=:css),
        ],
    ),
```
as argument to `makedocs`.
