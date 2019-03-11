---
layout: post
title:  "Capacidades de Micro Serviços: Como proteger o seu código e usar os super poderes da infra estrutura?"
categories: Microservices
excerpt_separator: <!--more-->
---
Todos que começam a usar microserviços se deparam com um problema enorme:

> Cada micro serviço deve possuir um conjunto de capacidades.

E a lista não é pequena.<!--more--> Tais capacidades incluem Descoberta, Invocação, Elasticidade, Resiliência, Monitoração, Rastreamento, Pipeline, Log distribuído, API e Autorização.

Na adoção antecipada de microserviços como parte da sua arquiteura, você não tinha muito o que fazer para solucionar tais capacidades. Então era sua responsabilidade resolver os problemas. O caso mais famoso desta épica façanha foi o Netflix OSS.

> Mas, qual é o problema com este tipo de abordagem?

O problema é que você acaba misturando no seu código funcionalidades de negócio com funções de rede e infra estrutura, o que torna a leitura, entendimento e manutenção uma dor de cabeça terrível e um trabalho estressante.

Além disso, outro problema decorrente do uso dessas bibliotecas: **você fica preso a tecnologia e linguagem de desenvolvimento, não tendo liberdade para seguir com outras linhas de implementação.**

Sem contar também que o tamanho da imagem do seu container ficará muito maior com a adição das bibliotecas em suas builds.

> Você sente que está tendo muito mais trabalho agora do que antes?

Reflita um instante sobre isso: Porque você está fazendo este tipo de controle no seu código? Isso é realmente necessário?

Eu sei que você adora lidar com problemas complexos e que esse pode ser o case da sua carreira. Mas por outro lado, toda construção complexa demanda tempo e isso cria uma pressão enorme, pois buscamos agilidade nas entregas. 

Então, vamos rever as capacidades que geralmente são resolivdas com código e descobrir alternativas que trarão mais agilidade nas suas entregas e por consequência menos estresse para você. 

# Service Discovery

Uma boa solução de {% include glossary.html id="service-discovery" label="Service Discovery" %} envolve o uso dos seguintes componentes de infra-estrutura:

* Service Registrar 
    * <a target="_blank" href="https://github.com/netflix/Prana">Prana</a>
    * <a target="_blank" href="https://github.com/gliderlabs/registrator">Registrator</a>
    * <a target="_blank" href="https://github.com/airbnb/nerve">Nerve</a>
* Service Registry
    * <a target="_blank" href="https://github.com/Netflix/eureka">Eureka</a>
    * <a target="_blank" href="https://github.com/coreos/etcd">etcd</a>
    * <a target="_blank" href="https://www.consul.io/">Consul</a>
    * <a target="_blank" href="http://zookeeper.apache.org/">Zookeeper</a>
* Proxy
    * <a target="_blank" href="https://www.nginx.com">NGINX</a>
    * <a target="_blank" href="https://aws.amazon.com/elasticloadbalancing/">AWS Elastic Load Balancer</a>
    * <a target="_blank" href="https://www.envoyproxy.io">Envoy</a>
    * <a target="_blank" href="https://github.com/airbnb/synapse">Synapse</a>
    * <a target="_blank" href="https://coredns.io">CoreDNS</a>

![Service Discovery Solution](/assets/images/posts/service-discovery.png)

<a target="_blank" href="https://github.com/kubernetes/kubernetes/blob/master/docs/design/architecture.md">Kubernetes</a> tem seu próprio mecanismo de Service Discovery nativo e o mesmo usa o etcd para fazer isso. <a target="_blank" href="http://aws.amazon.com/documentation/ecs">Amazon ECS</a> possui uma solução semelhante para Service Discovery também.

# Resiliência

Resiliência em micro serviços é alcançada com o uso do padrão de {% include glossary.html id="circuit-breaker" label="Circuit Breaker" %}. Uma solução bastante comum em código é o famoso Histryx desenvolvido pela Netflix.

Como você agora tem um Proxy para resolver seu problema de Service Discovery, você pode aproveitá-lo para dar resiliência para a sua solução de micro serviços. Por que não?

Resilience is achieved by using Circuit Breaker pattern. The most common solution is the Histryx by Netflix OSS. Again, if you are using a proxy for inter services communication, why not let the proxy to manage it for you? <a target="_blank" href="https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/circuit_breaking">Envoy</a> e <a target="_blank" href="https://www.nginx.com/blog/microservices-reference-architecture-nginx-circuit-breaker-pattern/">NGINX</a> possuem uma solução de circuit breaker nativa.

> Você deve estar se perguntando: Ok, qual é o ponto? Porque eu deveria mudar meu código para incorporar este tipo de infra estrutura, sendo que meus micro serviços estão funcionando perfeitamente?

Você somente faria uma mudanças dessa se você realmente pretende ter a liberdade de experimentar outras plataformas e linguagens. Neste caso ao invès de você construir um monte de código para suportar Service Discovery e Circuit Breaker, você simplesmente usaria a infra estrutura para tê-los.

Uma arquitetura de micro serviços não é fácil de se alcançar, porque são tantas as complexidades que você precisa lidar, que se torna um grande desafio alcançar seu estado da arte. Portanto, implementar e seguir com tais capacidades de infra estrutura, tornam este trabalho mais fácil e amigável para você.

# API

De longe, gerenciar as comunicações entre serviços é o trabalho mais difícil em uma arquitetura distribuída, porque você tem um monte de protocolos que você pode usar para resolver cada um dos problemas que você tem!

O modelo de comunicação mais usado é sem dúvidas o padrão REST. Mas eu te pergunto: Será que este é a melhor escolha para os requisitos, problemas e cenários que você tem? Sem dúvida uma grande discussão, certo? 

Por conta disso, eu convido você a se juntar a mim e a outros desenvolvedores num webinário exclusivo **Descubra os melhores protocolos de rede para uma arquitetura de micro serviços**  

Este webinário ao vivo será um ponto de partida para a série **Micro serviços direto das trincheiras**. Nesta série vamos discutir sobre problemas reais em projetos reais. Você pode trazer suas perguntas, problemas e interagir com a gente.

Este é um conteúdo especial que estará disponível apenas para os desenvolvedores que se inscreverem na lista. Então, se você ainda não é inscrito, faça isso agora! Deixe seu melhor e-mail e junte-se a centenas de desenvolvedores para ter acesso a conteúdos exclusivos e com prioridade. 

<p class="text-center">
    <a target="_blank" href="https://webinars.mrbraz.tech" class="btn btn-lg btn-primary">Eu quero me inscrever!</a>
</p>

Existem outras capacidades que você pode remover do seu código, porém, vamos tratar dessas capacidades num próximo artigo. Acredito que neste momento você tem bastante informação para pesquisar e conhecer. Como eu escrevi antes, estamos iniciando uma série e muito mais está por vir.

No próximo artigo da série vamos tratar de Logging, então, fique ligado. Se você quiser ser notificado quando um novo conteúdo estiver disponível, não se esqueça de fazer sua inscrição em nossa newsletter e me seguir nas redes sociais.