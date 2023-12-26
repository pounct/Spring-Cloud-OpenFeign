# Spring-Cloud-OpenFeign
# Spring Cloud OpenFeign
- Declarative REST Client: Feign

1. Include Feign

 <img src="images/challenger1init.png"/>

1. Getting Started

<pre><code class="hljs java"><button aria-live="Copy" class="button is-spring is-copy"></button><span class="hljs-meta">@SpringBootApplication</span>
<span class="hljs-meta">@EnableFeignClients</span>
<span class="hljs-keyword">public</span> <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">WebApplication</span> </span>{

	<span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-keyword">static</span> <span class="hljs-keyword">void</span> <span class="hljs-title">main</span><span class="hljs-params">(String[] args)</span> </span>{
		SpringApplication.run(WebApplication<span class="hljs-class">.<span class="hljs-keyword">class</span>, <span class="hljs-title">args</span>)</span>;
	}

	<span class="hljs-meta">@FeignClient</span>(<span class="hljs-string">"name"</span>)
	<span class="hljs-keyword">static</span> <span class="hljs-class"><span class="hljs-keyword">interface</span> <span class="hljs-title">NameService</span> </span>{
		<span class="hljs-meta">@RequestMapping</span>(<span class="hljs-string">"/"</span>)
		<span class="hljs-function"><span class="hljs-keyword">public</span> String <span class="hljs-title">getName</span><span class="hljs-params">()</span></span>;
	}
}
</code></pre>


# a concrete example: 
- we will create a challenger microservice with its dependencies
- pom.xml/gradle.build

  <img src="images/challenger1init.png"/>

- prepare the necessary models to receive the data in
  models package
  - class Challenge and subclasses...
  - 
in our case: 1 challenger is in relation with several challenges
we want to receive these challenges for each challenger

No create a service to request challenge microservice


<pre><code>
package challenger.services;

import java.util.UUID;

import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.hateoas.PagedModel;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;

import challenger.models.Challenge;

@FeignClient(name = "challenge") // name of service that expose endpoints : challenge-microservice
public interface ChallengeRestService {

	@GetMapping("/challenges/{id}") // ?projection=fullChallenge")
	public Challenge challengeById(@PathVariable UUID id);

	@GetMapping("/challenges/Challenger/{id}")
	public PagedModel<Challenge> allChallengesByUserId(@PathVariable UUID id);

}
</code></pre>

