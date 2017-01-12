<div class="row-fluid">
    <main id="content" role="main" class="span12">
    	<!-- Begin Content -->    
		<!-- Start K2 Category Layout -->
		<div id="k2Container" class="itemListView">
			<!-- Blocks for current category and subcategories -->
			<div class="itemListCategoriesBlock">
				<!-- Category block -->
				<div class="itemListCategory">
					<!-- Category title -->
					<h2>Produtos</h2>
					<!-- K2 Plugins: K2CategoryDisplay -->
					<div class="clr"></div>
				</div>
				<!-- Subcategories -->
		
				<div class="itemListSubCategories">
					<div style="display:inline-block; min-width: 300px;vertical-align:top;"class="left-bar">
						<div id="accordion">
				    		<ul>
				    		<?php 
								
								$args 		= array('orderby' => 'name', 'hide_empty' => 0, 'parent' => 1);
								$categories = get_categories( $args );
								$first 		= true;

								foreach ($categories as $category):
							?>
									<li>
										<div><?php echo $category->cat_name; ?></div>
										<ul>
											<?php 
				    						$theid = $category->term_id;
								    		$children = $wpdb->get_results( "SELECT term_id FROM $wpdb->term_taxonomy WHERE parent=$theid" );
								        	$no_children = count($children);
								        	?>
								        	<li><a href="<?php echo bloginfo('url'); ?>/<?php echo $category->slug; ?>">Todos</a></li>
								        	<?php 
								        	if ($no_children > 0): ?>

								        		<?php 
								        			$args2 				= array('orderby' => 'name', 'hide_empty' => 0, 'parent' => $category->term_id);
								        			$args2["parent"] 	= $category->term_id;
									    			$categories2 		= get_categories( $args2 );
									    		?>

									    		<?php foreach ($categories2 as $category2): ?>
													<li><a href="<?php echo bloginfo('url'); ?>/<?php echo $category2->slug; ?>"><?php echo $category2->cat_name; ?></a></li>
									    		<?php endforeach; ?>
								        	
								        	<?php endif; ?>
										</ul>
									</li>
							
				        	<?php endforeach; ?>
				        	</ul>
						</div>
					</div>
				<div style="display:inline-block;width:100%;vertical-align:top;margin-left: 160px;" class="right-content">
					<div class="clr"></div>
					<div class="itemList">
						
						<?php $query = new WP_Query(array('post_type' => array('produtos'))); ?>
			            <?php while ( $query->have_posts() ) : $query->the_post(); ?>
			                <?php $fotos = get_field('imagens'); ?>
			                <div id="itemListLeading">
							<div class="itemContainer" style="width:30%;">
								<div class="catItemView groupLeading">
									<div class="catItemBody">
	  									<div class="catItemImageBlock">
		  									<span class="catItemImage">
			    								<a href="<?php echo bloginfo('url'); ?>/produtos/<?php echo $post->post_name;?>" title="<?php the_title(); ?>">
			    									<img src="<?php echo $fotos[0]['imagem']['sizes']['thumbnail']; ?>" alt="Arm&aacute;rio alto fechado. C&oacute;digo-pz" style="width:236px; height:auto;" />
			    								</a>
		  									</span>
	  									</div>
									</div>
								</div>
								<style>
									div.catItemImageBlock{
										width: 200px;
									}
								</style>
							</div>
						</div>
			            <?php endwhile; ?>

					</div>
				</div>

				
				<style type="text/css">
					
				#accordion {
				    visibility:hidden;
				    position: absolute;
				    left: 10%;
				    width: 250px;
				}

				/* root UL */
				#accordion ul {
				    padding:0;
				    margin:0;
				    list-style:none;
				    background:#16a085; 
				}

				/*---------- Indents ------*/

				/*top-level*/
				#accordion .top > a, #accordion .top > div { 
				    padding-left:16px;
				    padding-top:12px;padding-bottom:12px;
				}

				/*2nd-level*/
				#accordion li li > a, #accordion li li > div {
				    padding-left:30px;
				    padding-top:8px;padding-bottom:8px;
				}

				/*3rd-level*/
				#accordion li li li > a, #accordion li li li > div { padding-left:50px; }


				/*---------- Other styles ------*/

				/* headings */
				#accordion li > div{
				    font-family:'Lucida Grande', Geneva, sans-serif;
				    font-weight:bold;
				    font-size:large;
				    color:#fff;
				}
				#accordion .active > div{
				    color:#fff;
				}

				#accordion li {
				    font-family:Arial, sans-serif;
				    font-size:13px;
					padding: 0;
				    margin:0;
				    overflow:hidden;
					cursor: pointer;
				}

				/* Add borders to the top LIs */
				#accordion .top {
				    /*border-bottom: 1px solid #444;*/
				}

				/* links */
				#accordion a {
				    color:#fff;
				    font-weight:normal;
				    font-size:13px;
				    text-decoration:none;
				    display:block;
				    line-height:1;
				    transition:all 0.3s;
				}
				#accordion a:hover {
				    color:#ccc;
				}
				#accordion a.active {
				    color:#ddd;
				    background-color:rgba(255,255,255,0.15);
				    font-weight:bold;
				}



				/* carets */
				#accordion .caret {
				    color:inherit;
				    float:right;
				    margin-top:8px;
				    margin-right:16px;
				    width: 0;
				    height: 0;
				    overflow:hidden;/*for IE6*/
				    border-style:solid;
				    border-width:6px;
				    position:relative;
				    
				    border-top:6px solid #fff;
				    border-bottom-width:0px;
				    border-left-color:transparent;
				    border-right-color: transparent;
				}  

				#accordion li li .caret {
				    margin-right:6px;
				    float:none;
				    display:inline-block;
				    margin-top:auto;
				    margin-bottom:4px;
				}  

				#accordion .caret.active {
				    margin-bottom:4px;
				    border-bottom-width:6px;
				    border-bottom-color:initial;
				    border-top: none;
				}

				#accordion li {
				    -ms-user-select:none;
				    -mos-user-select:none;
				    -webkit-user-select:none;
				    -o-user-select:none;
				    user-select:none;
				}
				.left-bar, div.itemListSubCategories{
					color: rgba(0,0,0,0);
				}
				#content
				{
				    min-height: 1010px;
				}

				.row-fluid .span12 
				{
				    width: 90% !important;
				    float: right !important;
				}
				</style>

				<link rel="stylesheet" href="<?php echo get_template_directory_uri(); ?>/assets/css/super-panel.css">
				<script language="JavaScript" src="<?php echo get_template_directory_uri(); ?>/assets/js/super-panel.js"></script>
				<script language="JavaScript" src="<?php echo get_template_directory_uri(); ?>/assets/js/accordion-menu.js"></script>

				<!-- JoomlaWorks "K2" (v2.6.9) | Learn more about K2 at http://getk2.org -->
				<div id="system-message-container">
					<div id="system-message"></div>
				</div>

		<!-- End Content -->
    </main>
</div>
<div class="wp-paginavi"><?php wp_pagenavi(); ?></div>
