# jsonpath

kubectl get nodes -o=jsonpath='{.items[*].metadata.name}'

kubectl get nodes -o=jsonpath='{.items[*].metadata.name}{.items[*].status.capacity.cpu}'

To format these 

kubectl get nodes -o=jsonpath='{.items[*].metadata.name} {"\n"} {.items[*].status.capacity.cpu}'
