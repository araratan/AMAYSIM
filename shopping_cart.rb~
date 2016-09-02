class ShoppingCart
  attr_accessor :hash

  def initialize
    self.hash = Array.new
  end

  def add(item, promo_code=nil)
    hash << {items: item, promo_code: promo_code}
  end

  def total
    tot, data_pck_plus = 0.0, 0
    included_data_pack = ""
    puts "========================================================================================"
    puts " Items Added                            Expected Cart Items"
    puts "========================================================================================"
    merge_items[0].each_with_index do |item, i|
      case item[:product_code]
        when "ult_small"
          if item[:cnt].to_i > 2
            group = (item[:cnt].to_i / 3).to_i
            remaining = (item[:cnt] - (group * 3))
            tot += ((group * 2) + remaining).to_f * 24.9
          else
            tot += item[:cnt].to_f * 24.9
          end
        when "ult_medium"
          data_pck_plus = item[:cnt]
          tot += item[:cnt].to_f * 29.9
        when "ult_large"
          if item[:cnt].to_i > 3
            tot += (item[:cnt].to_f * 39.9)
          else
            tot += (item[:cnt].to_f * 44.9)
          end
        when "1gb"
          tot += item[:cnt].to_f * 9.9
      end


      if data_pck_plus > 0
        included_data_pack = "#{data_pck_plus} x 1GB Data-pack"
      end

      if i == (merge_items[0].count - 1)
        puts "#{item[:item_added]}                     #{item[:item_added]}"
      else
        puts "#{item[:item_added]}            				 #{item[:item_added]}"
      end
    end
    puts "                                               #{included_data_pack}"
    puts "========================================================================================"
    puts "Expected Cart Total: #{merge_items[1] == true ? (tot.to_f - (tot.to_f * 0.1)).round(2) : tot.round(2)}"
  end

  private
  def merge_items
    ult_sm, ult_md, ult_lg, gb, avail_promo = 0, 0, 0, 0, false
    cart_items = []

    hash.each do |h|
      case h[:items]
        when "ult_small"
          ult_sm += 1
        when "ult_medium"
          ult_md += 1
        when "ult_large"
          ult_lg += 1
        when "1gb"
          gb += 1
      end

      if h[:promo_code]	== "I<3AMAYSIM"
        avail_promo = true
      end

    end

    if ult_sm > 0
      cart_items << {cnt: ult_sm, product_code: "ult_small", item_added: "#{ult_sm} x Unlimited 1GB", price_per_item: 24.90}
    end

    if ult_md > 0
      cart_items << {cnt: ult_md, product_code: "ult_medium", item_added: "#{ult_md} x Unlimited 2GB", price_per_item: 29.90}
    end

    if ult_lg > 0
      cart_items << {cnt: ult_lg, product_code: "ult_large", item_added: "#{ult_lg} x Unlimited 5GB", price_per_item: 44.90}
    end

    if gb > 0
      cart_items << {cnt: gb, product_code: "1gb", item_added: "#{ult_sm} x 1GB Data-pack", price_per_item: 9.90}
    end

    return cart_items, avail_promo
  end
end

