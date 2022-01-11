
Terrastate extension will graph the tf state file, but you can do it your self also with
```hcl
terraform plan -out my-plan.plan
terraform graph | dot -Tsvg > graph.svg

```

Thats for a simple svg, but if you need it in drawio you have to break out the bash and convert to xml

**Install graphviz and converter in ubuntu**
```bash
sudo apt install python3-pip graphviz graphviz-dev
pip3 install graphviz2drawio --upgrade
```

Output options can be found here:
<https://graphviz.org/docs/outputs/>






*ctrl-e in obsidian will show preview mode*

```
pip3 install graphviz2drawio --upgrade
```

Source for graphviz2drawIO
<https://github.com/hbmartin/graphviz2drawio>