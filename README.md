# Spring-Cloud-OpenFeign
# Spring Cloud OpenFeign
- Declarative REST Client: Feign

1. Include Feign

<pre><code class="language-xml hljs"><button aria-live="Copy" class="button is-spring is-copy"></button><span class="hljs-tag">&lt;<span class="hljs-name">properties</span>&gt;</span>
    <span class="hljs-tag">&lt;<span class="hljs-name">spring-cloud.version</span>&gt;</span>2023.0.0<span class="hljs-tag">&lt;/<span class="hljs-name">spring-cloud.version</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-name">properties</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-name">dependencyManagement</span>&gt;</span>
    <span class="hljs-tag">&lt;<span class="hljs-name">dependencies</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-name">dependency</span>&gt;</span>
            <span class="hljs-tag">&lt;<span class="hljs-name">groupId</span>&gt;</span>org.springframework.cloud<span class="hljs-tag">&lt;/<span class="hljs-name">groupId</span>&gt;</span>
            <span class="hljs-tag">&lt;<span class="hljs-name">artifactId</span>&gt;</span>spring-cloud-dependencies<span class="hljs-tag">&lt;/<span class="hljs-name">artifactId</span>&gt;</span>
            <span class="hljs-tag">&lt;<span class="hljs-name">version</span>&gt;</span>${spring-cloud.version}<span class="hljs-tag">&lt;/<span class="hljs-name">version</span>&gt;</span>
            <span class="hljs-tag">&lt;<span class="hljs-name">type</span>&gt;</span>pom<span class="hljs-tag">&lt;/<span class="hljs-name">type</span>&gt;</span>
            <span class="hljs-tag">&lt;<span class="hljs-name">scope</span>&gt;</span>import<span class="hljs-tag">&lt;/<span class="hljs-name">scope</span>&gt;</span>
        <span class="hljs-tag">&lt;/<span class="hljs-name">dependency</span>&gt;</span>
    <span class="hljs-tag">&lt;/<span class="hljs-name">dependencies</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-name">dependencyManagement</span>&gt;</span>
</code></pre>

<pre><code class="language-groovy hljs"><button aria-live="Copy" class="button is-spring is-copy"></button>plugins {
  id <span class="hljs-string">'java'</span>
  id <span class="hljs-string">'org.springframework.boot'</span> version <span class="hljs-string">'3.2.0'</span>
  id <span class="hljs-string">'io.spring.dependency-management'</span> version <span class="hljs-string">'1.1.4'</span>
}

repositories {
  mavenCentral()
}

ext {
  set(<span class="hljs-string">'springCloudVersion'</span>, <span class="hljs-string">"2023.0.0"</span>)
}

dependencyManagement {
  imports {
    mavenBom <span class="hljs-string">"org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"</span>
  }
}

</code></pre>

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
