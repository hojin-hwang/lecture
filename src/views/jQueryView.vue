<template>
  <section>
    <nav class="subject">
        <ul>
            <li><a href="#ajax">$.ajax()</a></li>
            <li><a href="#collaps">$ 충돌없이 사용하기</a></li>
            
        </ul>
    </nav>
    <main>

      <article class="code">
        <h3 id="ajax">$.ajax Method</h3>
        <pre v-highlightjs><code class="hljs javascript">jQuery.ajax( url [, settings] )
//url : 요청 URL (클라이언트가 HTTP 요청을 보낼 서버의 주소)
//data : 요청과 함께 서버에 보내는 string 또는 json
//success(data, textStatus, jqXHR) : 요청이 성공일때 실행되는 callback 함수
//dataType : 서버에서 내려온 data 형식. ( default : xml, json, script, text, html )
                
$.ajax({
    url: "/rest/1/pages/245", // 클라이언트가 HTTP 요청을 보낼 서버의 URL 주소
    data: { name: "홍길동" },  // HTTP 요청과 함께 서버로 보낼 데이터
    method: "GET",   // HTTP 요청 메소드(GET, POST 등)
    dataType: "json" // 서버에서 보내줄 데이터의 타입
})
// HTTP 요청이 성공하면 요청한 데이터가 done() 메소드로 전달됨.
.done(function(json) {
    $("&lt;h1&gt;").text(json.title).appendTo("body");
    $("&lt;div class=\"content\"&gt;").html(json.html).appendTo("body");
})
// HTTP 요청이 실패하면 오류와 상태에 관한 정보가 fail() 메소드로 전달됨.
.fail(function(xhr, status, errorThrown) {
    $("#text").html("오류가 발생했다.&lt;br&gt;")
    .append("오류명: " + errorThrown + "&lt;br&gt;")
    .append("상태: " + status);
})
// 
.always(function(xhr, status) {
    $("#text").html("요청이 완료되었습니다!");
});
</code></pre>
    </article>

    <article class="code">
        <h3 id="collaps">$ 충돌없이 사용</h3>
        <pre v-highlightjs><code class="hljs javascript">(($) => {
    //$ 사용가능
})(jQuery);

</code></pre>
    </article>

   

    </main>
  </section>
</template>

<style scoped>
main{
  padding: 0 1rem;
}
@media (min-width: 1024px) {
  section {
    min-height: 100vh;
    display: flex;
    align-items: flex-start;
    padding: 1rem 0;
  }
}
</style>
