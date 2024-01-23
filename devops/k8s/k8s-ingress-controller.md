#

k create ns ingress-controller-space

# Needs a config Map
k create cm ingress-controller-cm -n ingress-controller-space

# Needs two Service Account
k create sa ingress-controller -n ingress-controller-space
k create sa ingress-controller-admission  -n ingress-controller-space

# Role 1 for ingress-controller 
PolicyRule:
  Resources                           Non-Resource URLs  Resource Names  Verbs
  ---------                           -----------------  --------------  -----
events                              []                 []                           [create patch]
  configmaps                          []                 []                           [get list watch create]
  endpoints                           []                 []                           [get list watch]
  pods                                []                 []                           [get list watch]
  secrets                             []                 []                           [get list watch]
  services                            []                 []                           [get list watch]
  ingressclasses.networking.k8s.io    []                 []                           [get list watch]
  ingresses.networking.k8s.io         []                 []                           [get list watch]
  configmaps                          []                 [ingress-controller-leader]  [get update]
  namespaces                          []                 []                           [get]
  ingresses.networking.k8s.io/status  []                 []                           [update]
# Rule 2 for ingress-controller-admission  
PolicyRule:
  Resources  Non-Resource URLs  Resource Names  Verbs
  ---------  -----------------  --------------  -----
  secrets    []                 []              [get create]
# Cluster Rule 1 for ingress-controller 
PolicyRule:
  Resources                           Non-Resource URLs  Resource Names  Verbs
  ---------                           -----------------  --------------  -----
  events                              []                 []              [create patch]
  services                            []                 []              [get list watch]
  ingressclasses.networking.k8s.io    []                 []              [get list watch]
  ingresses.networking.k8s.io         []                 []              [get list watch]
  nodes                               []                 []              [list watch get]
  configmaps                          []                 []              [list watch]
  endpoints                           []                 []              [list watch]
  namespaces                          []                 []              [list watch]
  pods                                []                 []              [list watch]
  secrets                             []                 []              [list watch]
  ingresses.networking.k8s.io/status  []                 []              [update]

# ClusterRule 2 for ingress-controller-admission 
PolicyRule:
  Resources                                                     Non-Resource URLs  Resource Names  Verbs
  ---------                                        -----------------  --------------  -----
  validatingwebhookconfigurations.admissionregistration.k8s.io  []      []    [get update]

# create resources in ingress-controller.yaml
  