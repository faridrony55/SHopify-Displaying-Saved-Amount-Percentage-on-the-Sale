# SHopify-Displaying-Saved-Amount-Percentage-on-the-Sale


{% if template == 'product' %}

      {{ 'products.product.on_sale' | t }}
      
    {% else %}
    
      {% assign amount = 0 %}
      {% for variant in product.variants %}
      {% assign saving = variant.compare_at_price | minus: variant.price %}
      {% assign amount = saving | at_least: amount %}

      {% assign saving = variant.compare_at_price | minus: variant.price | times: 100 | divided_by: variant.compare_at_price | round %}
      {% assign percentage = saving | at_least: percentage %}

      {% endfor %} 
      {% capture saved_amount %}{{ amount | money_without_trailing_zeros }}{% endcapture %}


      You  Save  {{ saved_amount }} ( -{{ percentage }}% )
     
    {% endif %}
