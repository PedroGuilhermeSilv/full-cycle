## Kubernetes
- É um serviço open source utilizado para implantação, o dimensionamento e gerencionamento de aplicativos em contêiner.
- Normalmente acessamos via CLI: `kubecli`

- `Cluster` conjunto de máquinas(nodes)
- `Pods` unidade que contém os containers

## Pontos importantes

[Pontos Importantes](../kubernetes/img/pontos.png)

### Deployment
O k8 tem acesso ao recurso de cpu e máquina dos clusters e com isso ele pode gerenciar seus recursos então por exemplo, podemos 
utilizar réplicas de pods como segurança mas o kubernete não te permite exceder seu hardware.

[Deployment](../kubernetes/img/image.png)


## Replicaset
Quando subimos um pod e o mesmo der algum problema ou for deletado não iremos conseguir subir novamente. Entretanto, podemos utilizar réplicas e passar
o número minimo de apps que precisamos ent mesmo que um caia automaticamente sera gerado outro.
Porém temos um problema que para cada nova versão para os podis serem atualizados eles tem que ser reinicados então por isso usando o `Deployment`
o fluxo é deployment->replicaset->pod
O deployment gerencia as replicas para que quando haja alteração ele reiniciais gradualmente cada pod.

## Comandos

```cmd
kubectl config get-clusters
```

```cmd
kubectl config use-clusters nome_do_cluster
```


#F0088