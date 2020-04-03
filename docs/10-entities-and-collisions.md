# Entities and Collision#
---
 Randomly create 500 ninjas on the screen. Create a lookup table that contains the alpha property of ninjas that have collided. Present all ninjas with their alpha properties set.

```ruby
def tick args
  # destructure args into local variables
  grid, state, outputs = args.grid, args.state, args.outputs
  
  # use Game Toolkit's built in helper methods to create
  # adhoc entities
  state.ninjas ||= 500.map do
    state.new_entity(:ninja,
                    { rect: [grid.w.-(50) * rand,
                             grid.h.-(50) * rand,
                             50,
                             50] })
  end
  # use Ruby's powerful apis to determine collision
  state.collisions ||= state.ninja
                            .product
                            .reject { |n, n2| n == n2 }
                            .find_all { |n, n2| n.rect.intersects_rect?(n2.rect) }
                            .map { |n, _| [n.entity_id, 128] }
                            .pairs_to_hash
  #render everything to the screen
  outputs.sprites << state.ninjas.map do |n|
    [n.rect, 'dragonruby.png', 0,
     state.collisions[n.entity_id] || 255]
  end
end
```