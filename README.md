//######################################################################################

# opencart__cat--img
Изображения в категориях Opencart

файл catalog/controller/product/category.php
найти 

$data['categories'][] = array(
	'name' => $result['name'] . ($this->config->get('config_product_count') ? ' (' . $this->model_catalog_product->getTotalProducts($filter_data) . ')' : ''),
	'href' => $this->url->link('product/category', 'path=' . $this->request->get['path'] . '_' . $result['category_id'] . $url),
);

и заменить на 

if ($result['image']) {
	$image = $this->model_tool_image->resize($result['image'], 100, 100);
} else {
	$image = $this->model_tool_image->resize('placeholder.png', 100, 100);
}  

$data['categories'][] = array(
	'name' => $result['name'] . ($this->config->get('config_product_count') ? ' (' . $this->model_catalog_product->getTotalProducts($filter_data) . ')' : ''),
	'href' => $this->url->link('product/category', 'path=' . $this->request->get['path'] . '_' . $result['category_id'] . $url),
    'thumb'       => $image
);

файл catalog/view/theme/ваш_шаблон/template/product/category.twig
найти

{% for category in categories %}
   <li><a href="{{ category.href }}">{{ category.name }}</a></li>
{% endfor %}

и заменить на (ну или как у вас в дизайне там)

{% for category in categories %}
   <li><a href="{{ category.href }}">{{ category.name }}</a></li>
   <li><img src="{{ category.thumb }}" alt="{{ category.name }}" /></li>
{% endfor %}

//#################################################################################
