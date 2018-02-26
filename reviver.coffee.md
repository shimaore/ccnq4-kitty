    {fromJS,isKeyed} = Immutable = require 'immutable'

    sets = require './sets'

Which of the keys defined in our objects are actually Sets instread of Lists?

    module.exports = ccnq4_kitty_reviver = (key,value,path) ->
      if isKeyed value
        return value.toMap()
      else
        if sets.has key
          return value.toSet()
        else
          return value.toList()
