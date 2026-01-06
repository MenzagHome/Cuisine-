type: custom:button-card
entity: light.cuisine_2
icon: mdi:dishwasher-alert
name: |
  [[[
    if (states['input_boolean.lave_vaisselle_vide'].state == 'on') return 'Vider Lave-Vaisselle';
    return 'Cuisine';
  ]]]
show_name: true
show_state: false
styles:
  card:
    - height: 154px
    - border-radius: 50px
    - background-color: rgba(0, 0, 0, 0.7)
    - box-shadow: |
        [[[
          if (states['input_boolean.lave_vaisselle_vide'].state == 'on') return '0px 0px 9px 3px red';
          if (states['light.cuisine_2'].state == 'on') return '0px 0px 9px 3px var(--button-card-light-color)';
          return '0px 0px 9px 3px teal';
        ]]]
    - "--mdc-ripple-color": >
        [[[ return states['input_boolean.lave_vaisselle_vide'].state == 'on' ?
        'red' : 'aqua'; ]]]
  grid:
    - grid-template-areas: |
        [[[
          if (states['input_boolean.lave_vaisselle_vide'].state == 'on') return '"i i n n n n" "i i n n n n" "cui bar jarvis cafe micro thermo"';
          return '"imag imag n n n n" "imag imag n n n n" "cui bar jarvis cafe micro thermo"';
        ]]]
    - grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr
    - grid-template-rows: 1fr min-content min-content
  name:
    - font-size: >
        [[[ return states['input_boolean.lave_vaisselle_vide'].state == 'on' ?
        '20px' : '25px'; ]]]
    - font-weight: bold
    - text-transform: capitalize
    - transform: rotate(350deg)
    - color: |
        [[[
          if (states['input_boolean.lave_vaisselle_vide'].state == 'on') return 'red';
          if (states['light.cuisine_2'].state == 'on') return 'var(--button-card-light-color)';
          return 'lightblue';
        ]]]
  state:
    - color: red
    - font-size: 17px
    - transform: rotate(350deg)
    - justify-self: center
  icon:
    - width: 90%
    - color: red
    - transform: rotate(350deg)
    - animation: blink 2s ease infinite
  custom_fields:
    imag:
      - padding-bottom: 10px
      - justify-self: center
      - transform: rotate(350deg)
custom_fields:
  imag: |
    [[[
      if (states['input_boolean.lave_vaisselle_vide'].state == 'on') return '';
      
      if (states['light.cuisine_2'].state == 'off')
       return `<ha-icon icon="hue:room-kitchen-off" style="width:50%;color:lightblue"></ha-icon>`;

      if (states['light.jarvis_power'].state == 'on')
       return `<ha-icon icon="cil:dishwasher-silverware" style="width:75%; animation: rotating 5s alternate infinite;color: red"></ha-icon>`;
         
      return `<ha-icon icon="phu:kitchen" style="width:75%;color: var(--button-card-light-color)"></ha-icon>`;
     ]]]
  cui:
    card:
      type: custom:button-card
      entity: input_boolean.cuisine
      show_name: false
      icon: mdi:spotlight
      styles:
        card:
          - background: none
          - box-shadow: none
          - border: none
          - padding: 0
        icon:
          - width: 25px
          - color: >
              [[[ return states['input_boolean.cuisine'].state == 'on' ?
              'var(--button-card-light-color)' : 'lightblue'; ]]]
      tap_action:
        action: toggle
      hold_action:
        action: more-info
        entity: light.cuisine
  bar:
    card:
      type: custom:button-card
      entity: input_boolean.bar
      show_name: false
      icon: >-
        [[[ return states['input_boolean.bar'].state == 'on' ?
        'mdi:ceiling-light-multiple' : 'mdi:ceiling-light-multiple-outline'; ]]]
      styles:
        card:
          - background: none
          - box-shadow: none
          - border: none
          - padding: 0
        icon:
          - width: 25px
          - color: >
              [[[ return states['input_boolean.bar'].state == 'on' ?
              'var(--button-card-light-color)' : 'lightblue'; ]]]
      tap_action:
        action: toggle
      hold_action:
        action: more-info
        entity: light.bar
  jarvis:
    card:
      type: custom:button-card
      entity: sensor.fin_du_cycle_a
      show_icon: "[[[ return states['light.jarvis_power'].state != 'on'; ]]]"
      show_name: "[[[ return states['light.jarvis_power'].state == 'on'; ]]]"
      name: >-
        [[[ return states['light.jarvis_power'].state == 'on' ?
        states['sensor.fin_du_cycle_a'].state : ''; ]]]
      icon: |
        [[[
          if (states['sensor.jarvis_door']?.state === 'open') return 'mdi:dishwasher-alert';
          if (states['binary_sensor.do_pf_cuisine']?.state === 'on') return 'mdi:window-open-variant';
          if (states['input_boolean.lave_vaisselle_en_marche']?.state === 'on') return 'mdi:dishwasher-alert';
          return 'mdi:dishwasher';
        ]]]
      styles:
        card:
          - background: none
          - box-shadow: none
          - border: none
          - padding: 0
        name:
          - font-weight: bold
          - font-size: 14px
          - color: chartreuse
        icon:
          - width: 25px
          - color: |
              [[[
                if (states['sensor.jarvis_door']?.state === 'open' || states['binary_sensor.do_pf_cuisine']?.state === 'on') return 'red';
                if (states['input_boolean.lave_vaisselle_en_marche']?.state === 'on') return 'gold';
                return 'lightblue';
              ]]]
          - animation: |
              [[[
                if (states['sensor.jarvis_door']?.state === 'open') return 'blink 1s steps(1) infinite';
                if (states['binary_sensor.do_pf_cuisine']?.state === 'on' || states['input_boolean.lave_vaisselle_en_marche']?.state === 'on') return 'blink 2s ease infinite';
                return 'none';
              ]]]
      tap_action:
        action: call-service
        service: input_boolean.turn_on
        service_data:
          entity_id: input_boolean.lave_vaisselle_en_marche
        confirmation:
          text: Jarvis est-il opérationnel pour le lancement à 23h30 ?
      hold_action:
        action: fire-dom-event
        browser_mod:
          service: browser_mod.popup
          data:
            title: Sélection du Programme
            content:
              type: custom:mushroom-select-card
              entity: select.jarvis_active_program
              icon: cil:dishwasher-silverware
              name: Activation d'un programme Jarvis
              layout: vertical
              secondary_info: none
              icon_color: white
  cafe:
    card:
      type: custom:button-card
      entity: light.ptit_dej
      show_name: false
      icon: >-
        [[[ return states['light.ptit_dej'].state == 'on' ? 'mdi:coffee-maker' :
        'mdi:coffee-maker-outline'; ]]]
      styles:
        card:
          - background: none
          - box-shadow: none
          - border: none
          - padding: 0
        icon:
          - width: 25px
          - color: >-
              [[[ return states['light.ptit_dej'].state == 'on' ? 'gold' :
              'lightblue'; ]]]
      tap_action:
        action: toggle
  micro:
    card:
      type: custom:button-card
      entity: light.micro_ondes
      show_name: false
      icon: >-
        [[[ return states['light.micro_ondes'].state == 'on' ? 'mdi:microwave' :
        'mdi:microwave-off'; ]]]
      styles:
        card:
          - background: none
          - box-shadow: none
          - border: none
          - padding: 0
        icon:
          - width: 25px
          - color: >-
              [[[ return states['light.micro_ondes'].state == 'on' ? 'gold' :
              'lightblue'; ]]]
      tap_action:
        action: toggle
  thermo:
    card:
      type: custom:button-card
      entity: light.thermomix
      show_name: false
      icon: >-
        [[[ return states['light.thermomix'].state == 'on' ? 'mdi:blender' :
        'mdi:blender-outline'; ]]]
      styles:
        card:
          - background: none
          - box-shadow: none
          - border: none
          - padding: 0
        icon:
          - width: 25px
          - color: >-
              [[[ return states['light.thermomix'].state == 'on' ? 'gold' :
              'lightblue'; ]]]
      tap_action:
        action: toggle
state:
  - value: "on"
    id: light_on
  - value: "on"
    operator: template
    attribute: input_boolean.lave_vaisselle_vide
    id: alert_mode
double_tap_action:
  action: call-service
  service: input_boolean.turn_off
  service_data:
    entity_id: input_boolean.lave_vaisselle_vide
hold_action:
  action: navigate
  navigation_path: /lovelace/cuisine
tap_action:
  action: fire-dom-event
  honeycomb_menu:
    buttons:
      - entity: light.tablette_ha
        state:
          - value: "off"
            styles:
              icon:
                - color: lightblue
              card:
                - opacity: 0.7
                - background-color: teal
                - "--mdc-ripple-color": lightblue
                - "--mdc-ripple-press-opacity": 0.7
        styles:
          icon:
            - color: var(--button-card-light-color)
          card:
            - background-color: "#070235"
            - "--mdc-ripple-color": var(--button-card-light-color)
            - "--mdc-ripple-press-opacity": 0.7
        active: true
        tap_action:
          action: call-service
          service: light.toggle
          service_data:
            entity_id: light.tablette_ha
      - entity: light.baymax
        state:
          - value: "off"
            styles:
              icon:
                - color: lightblue
              card:
                - opacity: 0.7
                - background-color: teal
                - "--mdc-ripple-color": lightblue
                - "--mdc-ripple-press-opacity": 0.7
        styles:
          icon:
            - color: var(--button-card-light-color)
          card:
            - background-color: "#070235"
            - "--mdc-ripple-color": var(--button-card-light-color)
            - "--mdc-ripple-press-opacity": 0.7
        active: true
        tap_action:
          action: call-service
          service: light.toggle
          service_data:
            entity_id: light.baymax
      - icon: mdi:vanity-light
        entity: input_boolean.spots_cuisine
        state:
          - value: "off"
            icon: mdi:vanity-light
            styles:
              icon:
                - color: lightblue
              card:
                - opacity: 0.7
                - background-color: teal
                - "--mdc-ripple-color": lightblue
                - "--mdc-ripple-press-opacity": 0.7
        styles:
          icon:
            - color: var(--button-card-light-color)
          card:
            - background-color: "#070235"
            - "--mdc-ripple-color": var(--button-card-light-color)
            - "--mdc-ripple-press-opacity": 0.7
        active: true
        tap_action:
          action: call-service
          service: input_boolean.toggle
          service_data:
            entity_id: input_boolean.spots_cuisine
      - entity: cover.volet_roulant_cuisine
        icon: mdi:window-shutter-open
        state:
          - value: closed
            icon: mdi:window-shutter
            styles:
              icon:
                - color: lightblue
              card:
                - opacity: 0.7
                - background-color: teal
                - "--mdc-ripple-color": lightblue
                - "--mdc-ripple-press-opacity": 0.7
        styles:
          icon:
            - color: aqua
          card:
            - background-color: "#070235"
            - "--mdc-ripple-color": var(--button-card-light-color)
            - "--mdc-ripple-press-opacity": 0.7
        active: true
        tap_action:
          action: call-service
          service: cover.toggle
          service_data:
            entity_id: cover.volet_roulant_cuisine
        hold_action:
          action: call-service
          service: cover.stop_cover
          service_data:
            entity_id: cover.volet_roulant_cuisine
      - icon: mdi:microwave
        entity: light.micro_ondes
        state:
          - value: "off"
            icon: mdi:microwave-off
            styles:
              icon:
                - color: lightblue
              card:
                - opacity: 0.7
                - background-color: teal
                - "--mdc-ripple-color": lightblue
                - "--mdc-ripple-press-opacity": 0.7
        styles:
          icon:
            - color: aqua
          card:
            - background-color: "#070235"
            - "--mdc-ripple-color": var(--button-card-light-color)
            - "--mdc-ripple-press-opacity": 0.7
        active: true
        tap_action:
          action: call-service
          service: light.turn_on
          service_data:
            entity_id: light.micro_ondes
        hold_action:
          action: call-service
          service: light.turn_off
          service_data:
            entity_id: light.micro_ondes
      - entity: sensor.temperature_frigo
        styles:
          name:
            - color: aqua
          card:
            - background-color: teal
            - "--mdc-ripple-color": var(--button-card-light-color)
            - "--mdc-ripple-press-opacity": 0.7
        active: true
        show_state: true
        show_icon: false
