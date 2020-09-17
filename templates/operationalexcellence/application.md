# Application Operational Excellence

{{- $pillars := slice "operationalexcellence" -}}
{{- $lens := "application" -}}

{{- $filtered := where $.Site.Data.input "pillars" "intersect" $pillars -}}
{{- $filtered = where $filtered "lens" $lens }}

# Navigation Menu
{{- range $category := $.Site.Data.categories -}}
    {{- $questionsInCategory := where $filtered "category" $category.title -}}
    {{- if $questionsInCategory }}
- [{{ $category.title}}](#{{ replace (replaceRE "[^\\s\\d\\w]" "" $category.title) " " "-" }})
        {{- range $subCategory := $category.subCategories }}
            {{- $questionsInSubCategory := (and (where $filtered "category" $category.title) (where $filtered "subCategory" $subCategory.title)) -}}
            {{- if $questionsInSubCategory }}
  - [{{ $subCategory.title}}](#{{ replace (replaceRE "[^\\s\\d\\w]" "" $subCategory.title) " " "-" }})
            {{- end -}}
        {{- end -}}
    {{- end -}}
{{- end -}}

{{- range $category := $.Site.Data.categories -}}
    {{- $questionsInCategory := where $filtered "category" $category.title -}}
    {{- if $questionsInCategory }}
# {{ $category.title}}
    {{ range $subCategory := $category.subCategories -}}
        {{- $questionsInSubCategory := (and (where $filtered "category" $category.title) (where $filtered "subCategory" $subCategory.title)) -}}
        {{- if $questionsInSubCategory }}
## {{ $subCategory.title }}
            {{ range $question := $questionsInSubCategory }}
* {{ .title }}
  > {{ safeHTML .context }}
            {{ range .children }}
    - {{ .title }}
    > {{ safeHTML .context }}
                      {{ end }}
                  {{ end }}
              {{ end }}
            {{- end -}}
    {{- end -}}
{{- end -}}