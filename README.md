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

  <ul class="dependencies-list"><li><div class="dependency-item "><strong>Spring Web <span class="group">Web</span></strong><span class="description">Build web, including RESTful, applications using Spring MVC. Uses Apache Tomcat as the default embedded container.</span><a href="/" class="icon"><span class="a-content" tabindex="-1"><svg aria-hidden="true" focusable="false" data-icon="remove" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="icon-remove"><g id="Layer_1_1_"><path class="st0" d="M494,256c0,131.4-106.6,238-238,238S18,387.4,18,256S124.6,18,256,18S494,124.6,494,256z"></path></g><g id="Layer_2_1_"><line class="st1" x1="114.4" y1="260" x2="397.5" y2="260"></line></g></svg></span></a></div></li><li class="fade-enter-done"><div class="dependency-item "><strong>Spring Reactive Web <span class="group">Web</span></strong><span class="description">Build reactive web applications with Spring WebFlux and Netty.</span><a href="/" class="icon"><span class="a-content" tabindex="-1"><svg aria-hidden="true" focusable="false" data-icon="remove" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="icon-remove"><g id="Layer_1_1_"><path class="st0" d="M494,256c0,131.4-106.6,238-238,238S18,387.4,18,256S124.6,18,256,18S494,124.6,494,256z"></path></g><g id="Layer_2_1_"><line class="st1" x1="114.4" y1="260" x2="397.5" y2="260"></line></g></svg></span></a></div></li><li class="fade-enter-done"><div class="dependency-item "><strong>Spring Boot Actuator <span class="group">Ops</span></strong><span class="description">Supports built in (or custom) endpoints that let you monitor and manage your application - such as application health, metrics, sessions, etc.</span><a href="/" class="icon"><span class="a-content" tabindex="-1"><svg aria-hidden="true" focusable="false" data-icon="remove" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="icon-remove"><g id="Layer_1_1_"><path class="st0" d="M494,256c0,131.4-106.6,238-238,238S18,387.4,18,256S124.6,18,256,18S494,124.6,494,256z"></path></g><g id="Layer_2_1_"><line class="st1" x1="114.4" y1="260" x2="397.5" y2="260"></line></g></svg></span></a></div></li><li class="fade-enter-done"><div class="dependency-item "><strong>Spring Data MongoDB <span class="group">NoSQL</span></strong><span class="description">Store data in flexible, JSON-like documents, meaning fields can vary from document to document and data structure can be changed over time.</span><a href="/" class="icon"><span class="a-content" tabindex="-1"><svg aria-hidden="true" focusable="false" data-icon="remove" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="icon-remove"><g id="Layer_1_1_"><path class="st0" d="M494,256c0,131.4-106.6,238-238,238S18,387.4,18,256S124.6,18,256,18S494,124.6,494,256z"></path></g><g id="Layer_2_1_"><line class="st1" x1="114.4" y1="260" x2="397.5" y2="260"></line></g></svg></span></a></div></li><li class="fade-enter-done"><div class="dependency-item "><strong>Spring Data Reactive MongoDB <span class="group">NoSQL</span></strong><span class="description">Provides asynchronous stream processing with non-blocking back pressure for MongoDB.</span><a href="/" class="icon"><span class="a-content" tabindex="-1"><svg aria-hidden="true" focusable="false" data-icon="remove" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="icon-remove"><g id="Layer_1_1_"><path class="st0" d="M494,256c0,131.4-106.6,238-238,238S18,387.4,18,256S124.6,18,256,18S494,124.6,494,256z"></path></g><g id="Layer_2_1_"><line class="st1" x1="114.4" y1="260" x2="397.5" y2="260"></line></g></svg></span></a></div></li><li class="fade-enter-done"><div class="dependency-item "><strong>Lombok <span class="group">Developer Tools</span></strong><span class="description">Java annotation library which helps to reduce boilerplate code.</span><a href="/" class="icon"><span class="a-content" tabindex="-1"><svg aria-hidden="true" focusable="false" data-icon="remove" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="icon-remove"><g id="Layer_1_1_"><path class="st0" d="M494,256c0,131.4-106.6,238-238,238S18,387.4,18,256S124.6,18,256,18S494,124.6,494,256z"></path></g><g id="Layer_2_1_"><line class="st1" x1="114.4" y1="260" x2="397.5" y2="260"></line></g></svg></span></a></div></li><li class="fade-enter-done"><div class="dependency-item "><strong>Thymeleaf <span class="group">Template Engines</span></strong><span class="description">A modern server-side Java template engine for both web and standalone environments. Allows HTML to be correctly displayed in browsers and as static prototypes.</span><a href="/" class="icon"><span class="a-content" tabindex="-1"><svg aria-hidden="true" focusable="false" data-icon="remove" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="icon-remove"><g id="Layer_1_1_"><path class="st0" d="M494,256c0,131.4-106.6,238-238,238S18,387.4,18,256S124.6,18,256,18S494,124.6,494,256z"></path></g><g id="Layer_2_1_"><line class="st1" x1="114.4" y1="260" x2="397.5" y2="260"></line></g></svg></span></a></div></li><li class="fade-enter-done"><div class="dependency-item "><strong>Spring Configuration Processor <span class="group">Developer Tools</span></strong><span class="description">Generate metadata for developers to offer contextual help and "code completion" when working with custom configuration keys (ex.application.properties/.yml files).</span><a href="/" class="icon"><span class="a-content" tabindex="-1"><svg aria-hidden="true" focusable="false" data-icon="remove" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="icon-remove"><g id="Layer_1_1_"><path class="st0" d="M494,256c0,131.4-106.6,238-238,238S18,387.4,18,256S124.6,18,256,18S494,124.6,494,256z"></path></g><g id="Layer_2_1_"><line class="st1" x1="114.4" y1="260" x2="397.5" y2="260"></line></g></svg></span></a></div></li></ul>
