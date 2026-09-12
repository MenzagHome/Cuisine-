type: custom:button-card
entity: light.cuisine_2
show_name: false
show_state: false
show_icon: false
styles:
  card:
    - height: 170px
    - border-radius: 6px
    - background: |
        [[[
          if (states['input_boolean.lave_vaisselle_vide'].state === 'on') return 'rgba(255,23,68,0.03)';
          return states['light.cuisine_2'].state === 'on' ? 'rgba(255,193,7,0.03)' : 'rgba(0,229,255,0.03)';
        ]]]
    - border: |
        [[[
          if (states['input_boolean.lave_vaisselle_vide'].state === 'on') return '1px solid rgba(255,23,68,0.5)';
          return states['light.cuisine_2'].state === 'on' ? '1px solid rgba(255,193,7,0.22)' : '1px solid rgba(0,229,255,0.2)';
        ]]]
    - box-shadow: |
        [[[
          if (states['input_boolean.lave_vaisselle_vide'].state === 'on') return '0 0 40px rgba(255,23,68,0.18)';
          return states['light.cuisine_2'].state === 'on' ? '0 0 40px rgba(255,193,7,0.07)' : '0 0 40px rgba(0,229,255,0.06)';
        ]]]
    - padding: 0
    - overflow: visible
    - position: relative
  grid:
    - grid-template-areas: '"ico_main titre_cuisine" "b_bas b_bas"'
    - grid-template-columns: 95px 1fr
    - grid-template-rows: 102px 68px
custom_fields:
  titre_cuisine: |
    [[[
      const alert = states['input_boolean.lave_vaisselle_vide'].state === 'on';
      const isOn = states['light.cuisine_2'].state === 'on';
      const color = alert ? '#ff1744' : (isOn ? '#ffc107' : '#00e5ff');
      const label = alert ? 'Vider Lave-Vaisselle' : 'Cuisine';
      const fontSize = alert ? '17px' : '32px';
      const letterSpacing = alert ? '1px' : '4px';
      return `<div style="
        display: flex;
        align-items: center;
        justify-content: center;
        text-align: center;
        height: 100%;
        width: 100%;
        font-family: Orbitron, sans-serif;
        font-size: ${fontSize};
        font-weight: 700;
        letter-spacing: ${letterSpacing};
        color: ${color};
        text-shadow: 0 0 20px ${color}, 0 0 40px ${color}40;
        white-space: nowrap;
        padding: 0 8px;
      ">${label}</div>`;
    ]]]
  ico_main:
    card:
      type: custom:button-card
      entity: light.cuisine_2
      show_name: false
      show_state: false
      icon: |
        [[[
          if (states['input_boolean.lave_vaisselle_vide'].state === 'on') return 'mdi:dishwasher-alert';
          if (states['light.jarvis_power'].state === 'on') return 'cil:dishwasher-silverware';
          return states['light.cuisine_2'].state === 'on' ? 'phu:kitchen' : 'hue:room-kitchen-off';
        ]]]
      styles:
        card:
          - background: none
          - border: none
          - box-shadow: none
          - height: 102px
          - width: 95px
          - border-right: |
              [[[
                if (states['input_boolean.lave_vaisselle_vide'].state === 'on') return '1px solid rgba(255,23,68,0.3)';
                return states['light.cuisine_2'].state === 'on' ? '1px solid rgba(255,193,7,0.15)' : '1px solid rgba(0,229,255,0.12)';
              ]]]
          - border-radius: 0
        icon:
          - width: 75px
          - height: 75px
          - color: |
              [[[
                if (states['input_boolean.lave_vaisselle_vide'].state === 'on') return '#ff1744';
                if (states['light.jarvis_power'].state === 'on') return 'red';
                return states['light.cuisine_2'].state === 'on' ? '#ffc107' : '#00e5ff';
              ]]]
          - filter: |
              [[[
                if (states['input_boolean.lave_vaisselle_vide'].state === 'on') return 'drop-shadow(0 0 12px rgba(255,23,68,0.9))';
                if (states['light.jarvis_power'].state === 'on') return 'drop-shadow(0 0 12px rgba(255,0,0,0.7))';
                const c = states['light.cuisine_2'].state === 'on' ? 'rgba(255,193,7' : 'rgba(0,229,255';
                return `drop-shadow(0 0 12px ${c},0.9)) drop-shadow(0 0 25px ${c},0.4))`;
              ]]]
          - animation: |
              [[[
                if (states['input_boolean.lave_vaisselle_vide'].state === 'on') return 'blink 2 ease infinite';
                if (states['light.jarvis_power'].state === 'on') return 'rotating 5 alternate infinite';
                return 'none';
              ]]]
  b_bas:
    card:
      type: custom:button-card
      styles:
        card:
          - background: none
          - border: none
          - box-shadow: none
          - padding: 0 6px
          - height: 68px
          - display: flex
          - align-items: flex-end
          - overflow: visible
        grid:
          - grid-template-columns: repeat(6, 1fr)
          - grid-template-areas: '"b1 b2 b3 b4 b5 b6"'
          - gap: 4px
          - align-items: flex-end
      custom_fields:
        b1:
          card:
            type: custom:button-card
            entity: input_boolean.cuisine
            show_name: false
            show_state: false
            icon: mdi:spotlight
            state:
              - value: 'on'
                styles:
                  icon:
                    - color: '#ffc107'
                    - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
                  card:
                    - background: rgba(255,193,7,0.12)
                    - border: 1px solid rgba(255,193,7,0.45)
                    - border-top: none
                    - border-left: none
                    - box-shadow: >-
                        2px 4px 14px rgba(255,193,7,0.18), inset 0 -3px 0
                        #ffc107
                    - border-radius: 0 0 8px 0
                    - height: 52px
              - value: 'off'
                styles:
                  icon:
                    - color: rgba(0,229,255,0.35)
                    - filter: none
                  card:
                    - background: rgba(0,10,22,0.85)
                    - border: 1px solid rgba(0,229,255,0.13)
                    - border-top: none
                    - border-left: none
                    - box-shadow: none
                    - border-radius: 0 0 8px 0
                    - height: 42px
            tap_action:
              action: call-service
              service: input_boolean.toggle
              service_data:
                entity_id: input_boolean.cuisine
            hold_action:
              action: more-info
              entity: light.cuisine
        b2:
          card:
            type: custom:button-card
            entity: input_boolean.bar
            show_name: false
            show_state: false
            icon: >
              [[[ return states['input_boolean.bar'].state === 'on' ?
              'mdi:ceiling-light-multiple' :
              'mdi:ceiling-light-multiple-outline'; ]]]
            state:
              - value: 'on'
                styles:
                  icon:
                    - color: '#ffc107'
                    - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
                  card:
                    - background: rgba(255,193,7,0.12)
                    - border: 1px solid rgba(255,193,7,0.45)
                    - border-top: none
                    - border-left: none
                    - box-shadow: >-
                        2px 4px 14px rgba(255,193,7,0.18), inset 0 -3px 0
                        #ffc107
                    - border-radius: 0 0 8px 0
                    - height: 52px
              - value: 'off'
                styles:
                  icon:
                    - color: rgba(0,229,255,0.35)
                    - filter: none
                  card:
                    - background: rgba(0,10,22,0.85)
                    - border: 1px solid rgba(0,229,255,0.13)
                    - border-top: none
                    - border-left: none
                    - box-shadow: none
                    - border-radius: 0 0 8px 0
                    - height: 42px
            tap_action:
              action: call-service
              service: input_boolean.toggle
              service_data:
                entity_id: input_boolean.bar
            hold_action:
              action: more-info
              entity: light.bar
        b3:
          card:
            type: custom:button-card
            entity: sensor.fin_du_cycle_a
            show_name: false
            show_state: true
            icon: |
              [[[
                if (states['sensor.jarvis_door']?.state === 'open') return 'mdi:dishwasher-alert';
                if (states['binary_sensor.do_pf_cuisine']?.state === 'on') return 'mdi:window-open-variant';
                if (states['input_boolean.lave_vaisselle_en_marche']?.state === 'on') return 'mdi:dishwasher-alert';
                if (states['sensor.jarvis_etat']?.state === 'run') return 'cil:dishwasher-silverware';
                return 'mdi:dishwasher';
              ]]]
            styles:
              icon:
                - display: block
                - width: 22px
                - color: |
                    [[[
                      if (states['sensor.jarvis_door']?.state === 'open' || states['binary_sensor.do_pf_cuisine']?.state === 'on') return 'rgba(255,23,68,0.9)';
                      if (states['input_boolean.lave_vaisselle_en_marche']?.state === 'on' || states['sensor.jarvis_etat']?.state === 'run') return '#ffc107';
                      return 'rgba(0,229,255,0.35)';
                    ]]]
                - filter: |
                    [[[
                      if (states['sensor.jarvis_door']?.state === 'open' || states['binary_sensor.do_pf_cuisine']?.state === 'on') return 'drop-shadow(0 0 6px rgba(255,23,68,0.8))';
                      if (states['input_boolean.lave_vaisselle_en_marche']?.state === 'on' || states['sensor.jarvis_etat']?.state === 'run') return 'drop-shadow(0 0 6px rgba(255,193,7,0.8))';
                      return 'none';
                    ]]]
                - animation: |
                    [[[
                      if (states['sensor.jarvis_door']?.state === 'open') return 'blink 1 steps(1) infinite';
                      if (states['binary_sensor.do_pf_cuisine']?.state === 'on' || states['input_boolean.lave_vaisselle_en_marche']?.state === 'on') return 'blink 2 ease infinite';
                      return 'none';
                    ]]]
              state:
                - display: |
                    [[[
                      const doorOpen = states['sensor.jarvis_door']?.state === 'open';
                      const winOpen = states['binary_sensor.do_pf_cuisine']?.state === 'on';
                      const armed = states['input_boolean.lave_vaisselle_en_marche']?.state === 'on';
                      const running = states['sensor.jarvis_etat']?.state === 'run';
                      return (!doorOpen && !winOpen && !armed && running) ? 'block' : 'none';
                    ]]]
                - color: '#ffc107'
                - font-family: Orbitron, sans-serif
                - font-size: 11px
                - font-weight: 700
                - text-shadow: 0 0 6px rgba(255,193,7,0.8)
              card:
                - background: |
                    [[[
                      if (states['sensor.jarvis_door']?.state === 'open' || states['binary_sensor.do_pf_cuisine']?.state === 'on') return 'rgba(255,23,68,0.1)';
                      if (states['input_boolean.lave_vaisselle_en_marche']?.state === 'on' || states['sensor.jarvis_etat']?.state === 'run') return 'rgba(255,193,7,0.12)';
                      return 'rgba(0,10,22,0.85)';
                    ]]]
                - border: |
                    [[[
                      if (states['sensor.jarvis_door']?.state === 'open' || states['binary_sensor.do_pf_cuisine']?.state === 'on') return '1px solid rgba(255,23,68,0.45)';
                      if (states['input_boolean.lave_vaisselle_en_marche']?.state === 'on' || states['sensor.jarvis_etat']?.state === 'run') return '1px solid rgba(255,193,7,0.45)';
                      return '1px solid rgba(0,229,255,0.13)';
                    ]]]
                - border-top: none
                - border-left: none
                - box-shadow: |
                    [[[
                      if (states['sensor.jarvis_door']?.state === 'open' || states['binary_sensor.do_pf_cuisine']?.state === 'on') return '2px 4px 14px rgba(255,23,68,0.18), inset 0 -3px 0 #ff1744';
                      if (states['input_boolean.lave_vaisselle_en_marche']?.state === 'on' || states['sensor.jarvis_etat']?.state === 'run') return '2px 4px 14px rgba(255,193,7,0.18), inset 0 -3px 0 #ffc107';
                      return 'none';
                    ]]]
                - border-radius: 0 0 8px 0
                - height: |
                    [[[
                      if (states['sensor.jarvis_door']?.state === 'open' || states['binary_sensor.do_pf_cuisine']?.state === 'on' || states['input_boolean.lave_vaisselle_en_marche']?.state === 'on' || states['sensor.jarvis_etat']?.state === 'run') return '52px';
                      return '42px';
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
                  title: JARVIS
                  style: >
                    --popup-background: rgba(0, 5, 15, 0.96);
                    --popup-border-radius: 6px; --popup-border-color:
                    rgba(0,229,255,0.22); --popup-box-shadow: 0 0 40px
                    rgba(0,229,255,0.08); --ha-card-background: transparent;
                    --mdc-theme-surface: rgba(0, 5, 15, 0.96);
                    --primary-text-color: #00e5ff; --secondary-text-color:
                    rgba(0,229,255,0.55); --mdc-theme-primary: #00e5ff;
                    --paper-item-icon-color: #00e5ff; backdrop-filter:
                    blur(12px);
                  content:
                    type: custom:mushroom-select-card
                    entity: select.jarvis_active_program
                    icon: cil:dishwasher-silverware
                    name: Activation d'un programme Jarvis
                    layout: vertical
                    secondary_info: none
                    icon_color: white
        b4:
          card:
            type: custom:button-card
            entity: light.ptit_dej
            show_name: false
            show_state: false
            icon: >
              [[[ return states['light.ptit_dej'].state === 'on' ?
              'mdi:coffee-maker' : 'mdi:coffee-maker-outline'; ]]]
            state:
              - value: 'on'
                styles:
                  icon:
                    - color: '#ffc107'
                    - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
                  card:
                    - background: rgba(255,193,7,0.12)
                    - border: 1px solid rgba(255,193,7,0.45)
                    - border-top: none
                    - border-left: none
                    - box-shadow: >-
                        2px 4px 14px rgba(255,193,7,0.18), inset 0 -3px 0
                        #ffc107
                    - border-radius: 0 0 8px 0
                    - height: 52px
              - value: 'off'
                styles:
                  icon:
                    - color: rgba(0,229,255,0.35)
                    - filter: none
                  card:
                    - background: rgba(0,10,22,0.85)
                    - border: 1px solid rgba(0,229,255,0.13)
                    - border-top: none
                    - border-left: none
                    - box-shadow: none
                    - border-radius: 0 0 8px 0
                    - height: 42px
              - value: unavailable
                styles:
                  icon:
                    - color: rgba(0,229,255,0.35)
                    - filter: none
                  card:
                    - background: rgba(0,10,22,0.85)
                    - border: 1px solid rgba(0,229,255,0.13)
                    - border-top: none
                    - border-left: none
                    - box-shadow: none
                    - border-radius: 0 0 8px 0
                    - height: 42px
            tap_action:
              action: call-service
              service: light.toggle
              service_data:
                entity_id: light.ptit_dej
        b5:
          card:
            type: custom:button-card
            entity: light.micro_ondes
            show_name: false
            show_state: false
            icon: >
              [[[ return states['light.micro_ondes'].state === 'on' ?
              'mdi:microwave' : 'mdi:microwave-off'; ]]]
            state:
              - value: 'on'
                styles:
                  icon:
                    - color: '#ffc107'
                    - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
                  card:
                    - background: rgba(255,193,7,0.12)
                    - border: 1px solid rgba(255,193,7,0.45)
                    - border-top: none
                    - border-left: none
                    - box-shadow: >-
                        2px 4px 14px rgba(255,193,7,0.18), inset 0 -3px 0
                        #ffc107
                    - border-radius: 0 0 8px 0
                    - height: 52px
              - value: 'off'
                styles:
                  icon:
                    - color: rgba(0,229,255,0.35)
                    - filter: none
                  card:
                    - background: rgba(0,10,22,0.85)
                    - border: 1px solid rgba(0,229,255,0.13)
                    - border-top: none
                    - border-left: none
                    - box-shadow: none
                    - border-radius: 0 0 8px 0
                    - height: 42px
              - value: unavailable
                styles:
                  icon:
                    - color: rgba(0,229,255,0.35)
                    - filter: none
                  card:
                    - background: rgba(0,10,22,0.85)
                    - border: 1px solid rgba(0,229,255,0.13)
                    - border-top: none
                    - border-left: none
                    - box-shadow: none
                    - border-radius: 0 0 8px 0
                    - height: 42px
            tap_action:
              action: call-service
              service: light.toggle
              service_data:
                entity_id: light.micro_ondes
        b6:
          card:
            type: custom:button-card
            entity: light.thermomix
            show_name: false
            show_state: false
            icon: >
              [[[ return states['light.thermomix'].state === 'on' ?
              'mdi:blender' : 'mdi:blender-outline'; ]]]
            state:
              - value: 'on'
                styles:
                  icon:
                    - color: '#ffc107'
                    - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
                  card:
                    - background: rgba(255,193,7,0.12)
                    - border: 1px solid rgba(255,193,7,0.45)
                    - border-top: none
                    - border-left: none
                    - box-shadow: >-
                        2px 4px 14px rgba(255,193,7,0.18), inset 0 -3px 0
                        #ffc107
                    - border-radius: 0 0 8px 0
                    - height: 52px
              - value: 'off'
                styles:
                  icon:
                    - color: rgba(0,229,255,0.35)
                    - filter: none
                  card:
                    - background: rgba(0,10,22,0.85)
                    - border: 1px solid rgba(0,229,255,0.13)
                    - border-top: none
                    - border-left: none
                    - box-shadow: none
                    - border-radius: 0 0 8px 0
                    - height: 42px
              - value: unavailable
                styles:
                  icon:
                    - color: rgba(0,229,255,0.35)
                    - filter: none
                  card:
                    - background: rgba(0,10,22,0.85)
                    - border: 1px solid rgba(0,229,255,0.13)
                    - border-top: none
                    - border-left: none
                    - box-shadow: none
                    - border-radius: 0 0 8px 0
                    - height: 42px
            tap_action:
              action: call-service
              service: light.toggle
              service_data:
                entity_id: light.thermomix
  DecoLines: |
    [[[
      const alert = states['input_boolean.lave_vaisselle_vide'].state === 'on';
      const isOn = states['light.cuisine_2'].state === 'on';
      const c = alert ? '#ff1744' : (isOn ? '#ffc107' : '#00e5ff');
      const cOff = alert ? 'rgba(255,23,68,0.18)' : (isOn ? 'rgba(255,193,7,0.18)' : 'rgba(0,229,255,0.18)');
      const divLine = alert ? 'rgba(255,23,68,0.15)' : (isOn ? 'rgba(255,193,7,0.15)' : 'rgba(0,229,255,0.12)');
      const topLine = alert
        ? 'linear-gradient(90deg,transparent,#ff1744 30%,#ff1744 70%,transparent)'
        : (isOn
          ? 'linear-gradient(90deg,transparent,#ffc107 30%,#ffc107 70%,transparent)'
          : 'linear-gradient(90deg,transparent,#00e5ff 30%,#00e5ff 70%,transparent)');
      return `
        <style>
          @keyframes rotating { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
          @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.3} }
        </style>
        <div style="position:absolute;top:0;left:0;right:0;height:1px;background:${topLine};opacity:0.65;pointer-events:none;z-index:2;"></div>
        <div style="position:absolute;bottom:68px;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,${divLine},transparent);pointer-events:none;z-index:2;"></div>
        <div style="position:absolute;top:-1px;left:-1px;width:12px;height:12px;border-top:2px solid ${c};border-left:2px solid ${c};pointer-events:none;z-index:3;"></div>
        <div style="position:absolute;top:-1px;right:-1px;width:12px;height:12px;border-top:2px solid ${c};border-right:2px solid ${c};pointer-events:none;z-index:3;"></div>
        <div style="position:absolute;bottom:-1px;left:-1px;width:12px;height:12px;border-bottom:2px solid ${cOff};border-left:2px solid ${cOff};pointer-events:none;z-index:3;"></div>
        <div style="position:absolute;bottom:-1px;right:-1px;width:12px;height:12px;border-bottom:2px solid ${cOff};border-right:2px solid ${cOff};pointer-events:none;z-index:3;"></div>
      `;
    ]]]
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
    autoclose: true
    size: 210
    filter_radius: 100
    style:
      - background: rgba(0,5,15,0.92)
      - border: 1px solid rgba(0,229,255,0.25)
      - box-shadow: 0 0 40px rgba(0,229,255,0.1)
      - border-radius: 6px
    buttons:
      - entity: light.tablette_ha
        icon: mdi:tablet
        state:
          - value: 'on'
            styles:
              icon:
                - color: '#ffc107'
                - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
              card:
                - background: rgba(255,193,7,0.12)
                - border: 1px solid rgba(255,193,7,0.4)
                - box-shadow: 0 0 15px rgba(255,193,7,0.2)
          - value: 'off'
            styles:
              icon:
                - color: rgba(0,229,255,0.35)
              card:
                - background: rgba(0,10,22,0.85)
                - border: 1px solid rgba(0,229,255,0.2)
        tap_action:
          action: call-service
          service: light.toggle
          service_data:
            entity_id: light.tablette_ha
      - entity: light.baymax
        icon: mdi:robot-vacuum
        state:
          - value: 'on'
            styles:
              icon:
                - color: '#ffc107'
                - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
              card:
                - background: rgba(255,193,7,0.12)
                - border: 1px solid rgba(255,193,7,0.4)
                - box-shadow: 0 0 15px rgba(255,193,7,0.2)
          - value: 'off'
            styles:
              icon:
                - color: rgba(0,229,255,0.35)
              card:
                - background: rgba(0,10,22,0.85)
                - border: 1px solid rgba(0,229,255,0.2)
        tap_action:
          action: call-service
          service: light.toggle
          service_data:
            entity_id: light.baymax
      - icon: mdi:vanity-light
        entity: input_boolean.spots_cuisine
        state:
          - value: 'on'
            styles:
              icon:
                - color: '#ffc107'
                - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
              card:
                - background: rgba(255,193,7,0.12)
                - border: 1px solid rgba(255,193,7,0.4)
                - box-shadow: 0 0 15px rgba(255,193,7,0.2)
          - value: 'off'
            styles:
              icon:
                - color: rgba(0,229,255,0.35)
              card:
                - background: rgba(0,10,22,0.85)
                - border: 1px solid rgba(0,229,255,0.2)
        tap_action:
          action: call-service
          service: input_boolean.toggle
          service_data:
            entity_id: input_boolean.spots_cuisine
      - entity: cover.volet_roulant_cuisine
        icon: mdi:window-shutter-open
        state:
          - value: open
            styles:
              icon:
                - color: '#ffc107'
                - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
              card:
                - background: rgba(255,193,7,0.12)
                - border: 1px solid rgba(255,193,7,0.4)
                - box-shadow: 0 0 15px rgba(255,193,7,0.2)
          - value: closed
            icon: mdi:window-shutter
            styles:
              icon:
                - color: rgba(0,229,255,0.35)
              card:
                - background: rgba(0,10,22,0.85)
                - border: 1px solid rgba(0,229,255,0.2)
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
      - entity: light.micro_ondes
        icon: mdi:microwave
        state:
          - value: 'on'
            styles:
              icon:
                - color: '#ffc107'
                - filter: drop-shadow(0 0 6px rgba(255,193,7,0.8))
              card:
                - background: rgba(255,193,7,0.12)
                - border: 1px solid rgba(255,193,7,0.4)
                - box-shadow: 0 0 15px rgba(255,193,7,0.2)
          - value: 'off'
            icon: mdi:microwave-off
            styles:
              icon:
                - color: rgba(0,229,255,0.35)
              card:
                - background: rgba(0,10,22,0.85)
                - border: 1px solid rgba(0,229,255,0.2)
        tap_action:
          action: call-service
          service: light.toggle
          service_data:
            entity_id: light.micro_ondes
      - entity: sensor.temperature_frigo
        show_state: true
        show_icon: false
        show_name: false
        styles:
          state:
            - color: '#00e5ff'
            - font-family: Orbitron, sans-serif
            - font-size: 13px
            - filter: drop-shadow(0 0 6px rgba(0,229,255,0.6))
          card:
            - background: rgba(0,229,255,0.08)
            - border: 1px solid rgba(0,229,255,0.3)
            - box-shadow: 0 0 15px rgba(0,229,255,0.1)
